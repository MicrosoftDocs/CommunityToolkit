---
title: FlipHorizontalAnimation - .NET MAUI Community Toolkit
author: bijington
description: The FlipHorizontalAnimation flips a VisualElement horizontally and then back to its original orientation.
ms.date: 11/13/2026
---

# FlipHorizontalAnimation

The `FlipHorizontalAnimation` flips a `VisualElement` horizontally: the view rotates around its y-axis to `Rotation` and then back to the y-axis rotation it had before.

## Syntax

### XAML

For use within XAML the `FlipHorizontalAnimation` must be used in conjunction with the [`AnimationBehavior`](../behaviors/animation-behavior.md).

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the FlipHorizontalAnimation

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
                    <toolkit:FlipHorizontalAnimation Rotation="180" />
                </toolkit:AnimationBehavior.AnimationType>
            </toolkit:AnimationBehavior>
        </Label.Behaviors>
    </Label>

</ContentPage>
```

### C#

The `FlipHorizontalAnimation` can be used as follows in C#, here from a `Button.Clicked` handler:

```csharp
using CommunityToolkit.Maui.Animations;

public partial class MainPage : ContentPage
{
    public MainPage() => InitializeComponent();

    async void OnAnimateClicked(object? sender, EventArgs e)
    {
        var animation = new FlipHorizontalAnimation
        {
            Rotation = 180
        };

        await animation.Animate(TitleLabel);
    }
}
```

`TitleLabel` and `OnAnimateClicked` come from the page's XAML: a `Label` with `x:Name="TitleLabel"` and a `Button` with `Clicked="OnAnimateClicked"`, inside a layout such as `VerticalStackLayout`. Animate a view that is on screen: a view without a handler throws `ArgumentException`.

## Properties

| Property | Type | Description | Default value |
|----------|------|-------------|---------------|
| Rotation | `double` | The angle, in degrees, about the y-axis to turn the view **to**, not by. | `90` |
| Length | `uint` | The duration of the whole animation: half out, half back, in milliseconds. | `600` |
| Easing | [Easing](xref:Microsoft.Maui.Easing) | The easing function applied to each part of the animation. | `Easing.Linear` |

Values for `double` properties must be finite numbers: `NaN` and infinity are ignored.

## Behavior

- Returns the view to its original y-axis rotation when it ends.
- When triggered again while it runs, the new run continues from where the view is and ends at the original y-axis rotation. The run it interrupts leaves the view to the new run.
- Cancelling the token mid-run returns the view to its original y-axis rotation, then the awaited `Animate` throws `OperationCanceledException`. A token that is already cancelled throws before the view changes. Through `AnimationBehavior`, the command ends without an exception.
- Stopped while nothing takes over, for example by `CancelAnimations()` or another `AnimationBehavior` on the same view, the view returns to its original y-axis rotation at once and `Animate` completes.
- With the system's animations off, also when they are switched off mid-run, the view ends at its original y-axis rotation.

## Examples

You can find an example of this animation in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/AnimationBehaviorPage.xaml).

## API

You can find the source code for `FlipHorizontalAnimation` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Animations/FlipHorizontalAnimation.shared.cs).
