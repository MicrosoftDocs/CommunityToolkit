---
title: FlipVerticalAnimation - .NET MAUI Community Toolkit
author: bijington
description: The FlipVerticalAnimation flips a VisualElement vertically and then back to its original orientation.
ms.date: 11/13/2026
---

# FlipVerticalAnimation

The `FlipVerticalAnimation` flips a `VisualElement` vertically: the view rotates around its x-axis to `Rotation` and then back to the x-axis rotation it had before.

## Syntax

### XAML

For use within XAML the `FlipVerticalAnimation` must be used in conjunction with the [`AnimationBehavior`](../behaviors/animation-behavior.md).

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the FlipVerticalAnimation

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
                    <toolkit:FlipVerticalAnimation Rotation="180" />
                </toolkit:AnimationBehavior.AnimationType>
            </toolkit:AnimationBehavior>
        </Label.Behaviors>
    </Label>

</ContentPage>
```

### C#

The `FlipVerticalAnimation` can be used as follows in C#, here from a `Button.Clicked` handler:

```csharp
using CommunityToolkit.Maui.Animations;

public partial class MainPage : ContentPage
{
    public MainPage() => InitializeComponent();

    async void OnAnimateClicked(object? sender, EventArgs e)
    {
        var animation = new FlipVerticalAnimation
        {
            Rotation = 180
        };

        await animation.Animate(TitleLabel);
    }
}
```

The page's XAML must declare a `Label` with `x:Name="TitleLabel"`, so it is on screen when the animation runs, and a `Button` whose `Clicked` event is `OnAnimateClicked`. The XAML sample above shows only the animation, so add those two elements to it.

## Properties

| Property | Type | Description | Default value |
|----------|------|-------------|---------------|
| Rotation | `double` | The rotation, in degrees, around its x-axis to animate to. | `90` |
| Length | `uint` | The duration of the whole animation: half out, half back, in milliseconds. | `600` |
| Easing | [Easing](xref:Microsoft.Maui.Easing) | The easing function applied to each part of the animation. | `Easing.Linear` |

Values for `double` properties must be finite numbers: `NaN` and infinity are ignored.

## Behavior

- Returns the view to its original x-axis rotation when it ends.
- When triggered again while it runs, the new run continues from where the view is and ends at the original x-axis rotation. The run it interrupts stops where it is.
- Cancelling the token mid-run returns the view to its original x-axis rotation, then the awaited `Animate` throws `OperationCanceledException`. A token that is already cancelled throws before the view changes. Through `AnimationBehavior` that exception is unhandled unless you call [`SetShouldSuppressExceptionsInAnimations(true)`](../options.md#setshouldsuppressexceptionsinanimations).

## Examples

You can find an example of this animation in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/AnimationBehaviorPage.xaml).

## API

You can find the source code for `FlipVerticalAnimation` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Animations/FlipVerticalAnimation.shared.cs).
