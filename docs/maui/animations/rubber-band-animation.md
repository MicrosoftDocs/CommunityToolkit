---
title: RubberBandAnimation - .NET MAUI Community Toolkit
author: TheCodeTraveler
description: The RubberBandAnimation stretches a VisualElement wide and flat, then tall and thin, and wobbles it back to rest like a plucked rubber band.
ms.date: 11/13/2026
---

# RubberBandAnimation

The `RubberBandAnimation` stretches a `VisualElement` wide and flat, snaps it tall and thin and then wobbles it back to rest like a plucked rubber band.

## Syntax

### XAML

For use within XAML the `RubberBandAnimation` must be used in conjunction with the [`AnimationBehavior`](../behaviors/animation-behavior.md).

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the RubberBandAnimation

```xaml
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
    x:Class="MyLittleApp.MainPage">

    <Label Text="Tap this Label">
        <Label.Behaviors>
            <toolkit:AnimationBehavior AnimateOnTap="True">
                <toolkit:AnimationBehavior.AnimationType>
                    <toolkit:RubberBandAnimation />
                </toolkit:AnimationBehavior.AnimationType>
            </toolkit:AnimationBehavior>
        </Label.Behaviors>
    </Label>

</ContentPage>
```

### C#

The `RubberBandAnimation` can be used as follows in C#, here from a `Button.Clicked` handler:

```csharp
public partial class MainPage : ContentPage
{
    public MainPage() => InitializeComponent();

    async void OnAnimateClicked(object? sender, EventArgs e)
    {
        var animation = new RubberBandAnimation();

        await animation.Animate(TitleLabel);
    }
}
```

`TitleLabel` is a `Label` declared in the page's XAML with `x:Name="TitleLabel"`, so it is on screen when the animation runs.

## Properties

| Property | Type | Description | Default value |
|----------|------|-------------|---------------|
| Length | `uint` | The time, in milliseconds, over which to animate. | `1000` |
| Easing | [Easing](xref:Microsoft.Maui.Easing) | The easing function applied to the progress of the whole animation. See [Behavior](#behavior). | `Easing.Linear` |

## Behavior

- Changes only `ScaleX` and `ScaleY` (not `Scale`), relative to the view's own values, and returns them when it ends.
- It has no properties other than `Length` and `Easing`.
- A view runs one [attention seeker](index.md) at a time. Starting one, or triggering this one again, ends the running one and returns the view to rest first.
- Starting it stops a running `ScaleToAsync`, `ScaleXToAsync` or `ScaleYToAsync` of the view, including a running [`ScaleAnimation`](scale-animation.md).
- Cancelling the token mid-run returns the view to rest, then the awaited `Animate` throws `OperationCanceledException`. A token that is already cancelled throws before the view changes. Through `AnimationBehavior` that exception is unhandled unless you call [`SetShouldSuppressExceptionsInAnimations(true)`](../options.md#setshouldsuppressexceptionsinanimations).
- `Easing` warps the whole run, so use one that stays within 0..1 and only increases, such as `Linear`, `SinInOut` or `CubicOut`. `SpringOut` and `BounceOut` overshoot: they play every keyframe early, then hold the view still until `Length` ends. `SpringIn` holds the view still until late in the run. The view still ends at rest.

## Examples

You can find an example of this animation in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/AnimationBehaviorPage.xaml).

## API

You can find the source code for `RubberBandAnimation` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Animations/RubberBandAnimation.shared.cs).
