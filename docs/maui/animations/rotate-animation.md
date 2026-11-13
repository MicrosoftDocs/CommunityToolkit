---
title: RotateAnimation - .NET MAUI Community Toolkit
author: bijington
description: The RotateAnimation rotates a VisualElement from its original rotation to a specified rotation and then returns it to the original.
ms.date: 11/13/2026
---

# RotateAnimation

The `RotateAnimation` rotates a `VisualElement` around its z-axis to the specified rotation and then returns it to its original rotation.

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
                    <toolkit:RotateAnimation Rotation="360" />
                </toolkit:AnimationBehavior.AnimationType>
            </toolkit:AnimationBehavior>
        </Label.Behaviors>
    </Label>

</ContentPage>
```

### C#

The `RotateAnimation` can be used as follows in C#, here from a `Button.Clicked` handler:

```csharp
public partial class MainPage : ContentPage
{
    public MainPage() => InitializeComponent();

    async void OnAnimateClicked(object? sender, EventArgs e)
    {
        var animation = new RotateAnimation
        {
            Rotation = 360
        };

        await animation.Animate(TitleLabel);
    }
}
```

`TitleLabel` is a `Label` declared in the page's XAML with `x:Name="TitleLabel"`, so it is on screen when the animation runs.

## Properties

| Property | Type | Description | Default value |
|----------|------|-------------|---------------|
| Rotation | `double` | The rotation, in degrees, to animate to. | `180` |
| Length | `uint` | The time, in milliseconds, to rotate to `Rotation`; the view then snaps back. | `200` |
| Easing | [Easing](xref:Microsoft.Maui.Easing) | The easing function applied to the rotation to `Rotation`. | `Easing.Linear` |

Values for `double` properties must be finite numbers: `NaN` and infinity are ignored.

## Behavior

- Rotates to `Rotation` over `Length`, then sets the view straight back to its original rotation. Use `360` for a seamless full turn.
- When triggered again while it runs, the new run continues from where the view is and ends at the original rotation. The run it interrupts stops where it is.
- Cancelling the token mid-run returns the view to its original rotation, then the awaited `Animate` throws `OperationCanceledException`. A token that is already cancelled throws before the view changes. Through `AnimationBehavior` that exception is unhandled unless you call [`SetShouldSuppressExceptionsInAnimations(true)`](../options.md#setshouldsuppressexceptionsinanimations).

## Examples

You can find an example of this animation in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/AnimationBehaviorPage.xaml).

## API

You can find the source code for `RotateAnimation` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Animations/RotateAnimation.shared.cs).
