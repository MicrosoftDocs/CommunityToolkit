---
title: WobbleAnimation - .NET MAUI Community Toolkit
author: TheCodeTraveler
description: The WobbleAnimation sways a VisualElement from side to side with a matching tilt, each sway smaller than the last.
ms.date: 11/13/2026
---

# WobbleAnimation

The `WobbleAnimation` sways a `VisualElement` from side to side with a matching tilt. Each sway is smaller than the last, until the view settles.

## Syntax

### XAML

For use within XAML the `WobbleAnimation` must be used in conjunction with the [`AnimationBehavior`](../behaviors/animation-behavior.md).

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the WobbleAnimation

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
                    <toolkit:WobbleAnimation Distance="40" RotationAngle="8" />
                </toolkit:AnimationBehavior.AnimationType>
            </toolkit:AnimationBehavior>
        </Label.Behaviors>
    </Label>

</ContentPage>
```

### C#

The `WobbleAnimation` can be used as follows in C#, here from a `Button.Clicked` handler:

```csharp
public partial class MainPage : ContentPage
{
    public MainPage() => InitializeComponent();

    async void OnAnimateClicked(object? sender, EventArgs e)
    {
        var animation = new WobbleAnimation
        {
            Distance = 40,
            RotationAngle = 8
        };

        await animation.Animate(TitleLabel);
    }
}
```

`TitleLabel` is a `Label` declared in the page's XAML with `x:Name="TitleLabel"`, so it is on screen when the animation runs.

## Properties

| Property | Type | Description | Default value |
|----------|------|-------------|---------------|
| Distance | `double` | The distance of the first sway, in device-independent units. Later sways are 0.8, 0.6, 0.4 and 0.2 of it. A negative value sways to the right first. | `25` |
| RotationAngle | `double` | The angle, in degrees, of the first tilt. Later tilts are 0.6, 0.6, 0.4 and 0.2 of it. A negative value tilts the other way first. | `5` |
| Length | `uint` | The time, in milliseconds, over which to animate. | `1000` |
| Easing | [Easing](xref:Microsoft.Maui.Easing) | The easing function applied to the progress of the whole animation. See [Behavior](#behavior). | `Easing.Linear` |

Values for `double` properties must be finite numbers: `NaN` and infinity are ignored.

## Behavior

- Changes only `TranslationX` and `Rotation`, relative to the view's own values, and returns them when it ends.
- A view runs one [attention seeker](index.md) at a time. Starting one, or triggering this one again, ends the running one and returns the view to rest first.
- Starting it stops a running `RotateToAsync` of the view, including a running [`RotateAnimation`](rotate-animation.md). A running `TranslateToAsync` keeps running, because that animation drives both axes in one handle.
- Cancelling the token mid-run returns the view to rest, then the awaited `Animate` throws `OperationCanceledException`. A token that is already cancelled throws before the view changes. Through `AnimationBehavior` that exception is unhandled unless you call [`SetShouldSuppressExceptionsInAnimations(true)`](../options.md#setshouldsuppressexceptionsinanimations).
- `Easing` warps the whole run, so use one that stays within 0..1 and only increases, such as `Linear`, `SinInOut` or `CubicOut`. `SpringOut` and `BounceOut` overshoot: they play every keyframe early, then hold the view still until `Length` ends. `SpringIn` holds the view still until late in the run. The view still ends at rest.

## Examples

You can find an example of this animation in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/AnimationBehaviorPage.xaml).

## API

You can find the source code for `WobbleAnimation` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Animations/WobbleAnimation.shared.cs).
