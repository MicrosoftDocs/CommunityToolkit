---
title: Animations - .NET MAUI Community Toolkit
author: bijington
description: The .NET MAUI Community Toolkit provides a collection of pre-built, reusable animations to make developers lives easier.
ms.date: 11/13/2026
---

# Animations

The .NET Multi-platform App UI (.NET MAUI) animation classes target different properties of visual elements, with a typical basic animation progressively changing a property from one value to another over a period of time.

For further information on Animations please refer to the [.NET MAUI documentation](/dotnet/maui/user-interface/animation/basic).

## .NET MAUI Community Toolkit Animations

The .NET MAUI Community Toolkit provides a collection of pre-built, reusable animations that can be used in both C# and XAML. Here are the animations provided by the toolkit:

| Animation | Description |
| --------- | ----------- |
| [`BounceAnimation`](../animations/bounce-animation.md) | The `BounceAnimation` hops the view up and down, with two smaller hops after the first. |
| [`FadeAnimation`](../animations/fade-animation.md) | The `FadeAnimation` animates the opacity of the view to a specified opacity and then back to the original. |
| [`FlipHorizontalAnimation`](../animations/flip-horizontal-animation.md) | The `FlipHorizontalAnimation` flips the view around its y-axis and then back. |
| [`FlipVerticalAnimation`](../animations/flip-vertical-animation.md) | The `FlipVerticalAnimation` flips the view around its x-axis and then back. |
| [`HeartbeatAnimation`](../animations/heartbeat-animation.md) | The `HeartbeatAnimation` beats the view twice like a heart, growing and shrinking it each time. |
| [`RotateAnimation`](../animations/rotate-animation.md) | The `RotateAnimation` rotates the view to a specified rotation and returns it to its original rotation. |
| [`RubberBandAnimation`](../animations/rubber-band-animation.md) | The `RubberBandAnimation` stretches the view wide and flat, then tall and thin, and wobbles it back to rest. |
| [`ScaleAnimation`](../animations/scale-animation.md) | The `ScaleAnimation` scales the view to a specified scale and then back to the original. |
| [`ShakeAnimation`](../animations/shake-animation.md) | The `ShakeAnimation` shakes the view sideways, with each swing smaller than the last. |
| [`SwingAnimation`](../animations/swing-animation.md) | The `SwingAnimation` swings the view like a sign hanging from its top edge. |
| [`TadaAnimation`](../animations/tada-animation.md) | The `TadaAnimation` shrinks the view with a tilt, grows it while it wiggles and then settles it. |
| [`WobbleAnimation`](../animations/wobble-animation.md) | The `WobbleAnimation` sways the view from side to side with a matching tilt, each sway smaller. |

## Behavior shared by the toolkit's animations

- **Cancelling:** cancelling the token mid-run returns the view to its original values, then the awaited `Animate` throws `OperationCanceledException`. A token that is already cancelled throws before the view changes.
- **Any thread:** `Animate` can be called from any thread. The animations run on the view's dispatcher.
- **System animations off:** with the system's animations off (for example Reduce Motion on iOS and Mac Catalyst, "Remove animations" on Android, or "Animation effects" off on Windows), `Animate` completes at once and leaves the view at its original values.

### Attention seekers

Bounce, Heartbeat, RubberBand, Shake, Swing, Tada and Wobble are attention seekers.

- They work relative to the view's original values and return every value they change when they end.
- A view runs one attention seeker at a time. Starting one ends the running one first.
- Calling `Animate` on one stops a running `RotateToAsync`, `ScaleToAsync`, `ScaleXToAsync` or `ScaleYToAsync` of the properties it animates, including a running `RotateAnimation` or `ScaleAnimation`. It does not stop a running `TranslateToAsync`, because that animation drives both axes in one handle. Through `AnimationBehavior` it does, see [AnimationBehavior](../behaviors/animation-behavior.md).
- `Easing` warps the whole run, so use one that stays within 0..1 and only increases, such as `Linear`, `SinInOut` or `CubicOut`. `SpringOut` plays every keyframe early, then holds the view still until `Length` ends. `BounceOut` replays the end of the run as it bounces. `SpringIn` holds the view still until late in the run. `ShakeAnimation` is the exception: its `Easing` shapes each movement.

## Creating custom animations

All animations provided by the .NET MAUI Community Toolkit inherit from our `BaseAnimation` class. In order to create any custom animation of your choosing you can do the same. A custom animation does not get the behavior described in [Behavior shared by the toolkit's animations](#behavior-shared-by-the-toolkits-animations).

The following example shows how to change the `BackgroundColor` of a `VisualElement` using our very own [`BackgroundColorTo`](../extensions/color-animation-extensions.md#backgroundcolorto) extension method.

```csharp
using CommunityToolkit.Maui.Animations;
using CommunityToolkit.Maui.Extensions;

partial class PaintTheRainbowAnimation : BaseAnimation
{
    public override async Task Animate(VisualElement view, CancellationToken token = default)
    {
        await view.BackgroundColorTo(Colors.Red, token: token);
        await view.BackgroundColorTo(Colors.Orange, token: token);
        await view.BackgroundColorTo(Colors.Yellow, token: token);
        await view.BackgroundColorTo(Colors.Green, token: token);
        await view.BackgroundColorTo(Colors.Blue, token: token);
        await view.BackgroundColorTo(Colors.Indigo, token: token);
        await view.BackgroundColorTo(Colors.Violet, token: token);
    }
}
```
