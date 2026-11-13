---
title: SwingAnimation - .NET MAUI Community Toolkit
author: TheCodeTraveler
description: The SwingAnimation swings a VisualElement like a sign hanging from its top edge.
ms.date: 11/13/2026
---

# SwingAnimation

The `SwingAnimation` swings a `VisualElement` like a sign hanging from its top edge: first `RotationAngle` degrees one way, then back two-thirds the other way, a third each way, and then to rest.

## Syntax

### XAML

For use within XAML the `SwingAnimation` must be used in conjunction with the [`AnimationBehavior`](../behaviors/animation-behavior.md).

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the SwingAnimation

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
                    <toolkit:SwingAnimation RotationAngle="25" />
                </toolkit:AnimationBehavior.AnimationType>
            </toolkit:AnimationBehavior>
        </Label.Behaviors>
    </Label>

</ContentPage>
```

### C#

The `SwingAnimation` can be used as follows in C#, here from a `Button.Clicked` handler:

```csharp
using CommunityToolkit.Maui.Animations;

public partial class MainPage : ContentPage
{
    public MainPage() => InitializeComponent();

    async void OnAnimateClicked(object? sender, EventArgs e)
    {
        var animation = new SwingAnimation
        {
            RotationAngle = 25
        };

        await animation.Animate(TitleLabel);
    }
}
```

`TitleLabel` and `OnAnimateClicked` come from the page's XAML: a `Label` with `x:Name="TitleLabel"` and a `Button` with `Clicked="OnAnimateClicked"`, inside a layout such as `VerticalStackLayout`.

## Properties

| Property | Type | Description | Default value |
|----------|------|-------------|---------------|
| RotationAngle | `double` | The angle, in degrees, of the first swing. The next swings are -2/3, +1/3 and -1/3 of it. A positive value swings clockwise first; a negative value swings counter-clockwise first. | `15` |
| Length | `uint` | The time, in milliseconds, over which to animate. | `1000` |
| Easing | [Easing](xref:Microsoft.Maui.Easing) | The easing function applied to the progress of the whole animation. See [Behavior](#behavior). | `Easing.Linear` |

Values for `double` properties must be finite numbers: `NaN` and infinity are ignored.

## Behavior

- Changes `Rotation`, relative to the view's own rotation, and sets `AnchorY` to `0` (the top edge) while it runs. Both return to their original values when it ends. A view whose original `Scale`, `ScaleY`, `Rotation`, `RotationX` or `RotationY` is not the identity appears shifted while the anchor is at the top.
- A view runs one [attention seeker](index.md#attention-seekers) at a time. Starting one, or triggering this one again, ends the running one and returns the view to rest first.
- Calling `Animate` stops a running `RotateToAsync` of the view, including a running [`RotateAnimation`](rotate-animation.md).
- Cancelling the token mid-run returns the view to rest, then the awaited `Animate` throws `OperationCanceledException`. A token that is already cancelled throws before the view changes. Through `AnimationBehavior`, the command ends without an exception.
- `Easing` warps the whole run, so use one that stays within 0..1 and only increases, such as `Linear`, `SinInOut` or `CubicOut`. `SpringOut` plays every keyframe early, then holds the view still until `Length` ends. `BounceOut` runs through the keyframes in about the first third of `Length`, then moves the view back and forth within the last keyframe. `SpringIn` holds the view still until late in the run. The view still ends at rest.

## Examples

You can find an example of this animation in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/AnimationBehaviorPage.xaml).

## API

You can find the source code for `SwingAnimation` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Animations/SwingAnimation.shared.cs).
