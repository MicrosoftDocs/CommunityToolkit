---
title: RotateAnimation - .NET MAUI Community Toolkit
author: bijington
description: The RotateAnimation turns a VisualElement by a specified angle from its own rotation and then returns it to the original rotation.
ms.date: 11/13/2026
---

# RotateAnimation

The `RotateAnimation` turns a `VisualElement` around its z-axis by the specified angle, measured from the view's own rotation, and then returns it to its original rotation. The default is one full 360 degree turn.

## Syntax

### XAML

For use within XAML the `RotateAnimation` must be used in conjunction with the [`AnimationBehavior`](../behaviors/animation-behavior.md).

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the RotateAnimation

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
                    <toolkit:RotateAnimation />
                </toolkit:AnimationBehavior.AnimationType>
            </toolkit:AnimationBehavior>
        </Label.Behaviors>
    </Label>

</ContentPage>
```

### C#

The `RotateAnimation` can be used as follows in C#, here from a `Button.Clicked` handler:

```csharp
using CommunityToolkit.Maui.Animations;

public partial class MainPage : ContentPage
{
    public MainPage() => InitializeComponent();

    async void OnAnimateClicked(object? sender, EventArgs e)
    {
        var animation = new RotateAnimation();

        await animation.Animate(TitleLabel);
    }
}
```

`TitleLabel` and `OnAnimateClicked` come from the page's XAML: a `Label` with `x:Name="TitleLabel"` and a `Button` with `Clicked="OnAnimateClicked"`, inside a layout such as `VerticalStackLayout`. Animate a view that is on screen: a view without a handler throws `ArgumentException`.

## Properties

| Property | Type | Description | Default value |
|----------|------|-------------|---------------|
| Rotation | `double` | The angle, in degrees, to turn the view by from its original rotation. A negative angle turns it counterclockwise. | `360` |
| Length | `uint` | The time, in milliseconds, of the turn. The view then returns to its original rotation at once, which is invisible for a multiple of 360. | `400` |
| Easing | [Easing](xref:Microsoft.Maui.Easing) | The easing function applied to the turn. | `Easing.Linear` |

Values for `double` properties must be finite numbers: `NaN` and infinity are ignored.

## Behavior

- Turns the view by `Rotation` degrees from its own rotation over `Length`, then sets it straight back to its original rotation. The default 360 is a seamless full turn from any rotation.
- When triggered again while it runs, the new run finishes the same turn, `Rotation` degrees from the rotation the view had before the first run, so repeated taps never leave it turned. The run it interrupts leaves the view to the new run.
- Cancelling the token mid-run returns the view to its original rotation, then the awaited `Animate` throws `OperationCanceledException`. A token that is already cancelled throws before the view changes. Through `AnimationBehavior`, the command ends without an exception.
- Stopped while nothing takes over, for example by `CancelAnimations()` or another `AnimationBehavior` on the same view, the view returns to its original rotation at once and `Animate` completes.
- With the system's animations off, also when they are switched off mid-run, the view ends at its original rotation.

## Examples

You can find an example of this animation in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/AnimationBehaviorPage.xaml).

## API

You can find the source code for `RotateAnimation` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Animations/RotateAnimation.shared.cs).
