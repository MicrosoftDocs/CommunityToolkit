---
title: ScaleAnimation - .NET MAUI Community Toolkit
author: bijington
description: The ScaleAnimation scales a VisualElement from its original scale to a specified scale and then back to the original.
ms.date: 11/13/2026
---

# ScaleAnimation

The `ScaleAnimation` scales a `VisualElement` from its original scale to a specified scale and then back to the original.

## Syntax

### XAML

For use within XAML the `ScaleAnimation` must be used in conjunction with the [`AnimationBehavior`](../behaviors/animation-behavior.md).

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ScaleAnimation

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
                    <toolkit:ScaleAnimation Scale="1.5" />
                </toolkit:AnimationBehavior.AnimationType>
            </toolkit:AnimationBehavior>
        </Label.Behaviors>
    </Label>

</ContentPage>
```

### C#

The `ScaleAnimation` can be used as follows in C#, here from a `Button.Clicked` handler:

```csharp
using CommunityToolkit.Maui.Animations;

public partial class MainPage : ContentPage
{
    public MainPage() => InitializeComponent();

    async void OnAnimateClicked(object? sender, EventArgs e)
    {
        var animation = new ScaleAnimation
        {
            Scale = 1.5
        };

        await animation.Animate(TitleLabel);
    }
}
```

`TitleLabel` and `OnAnimateClicked` come from the page's XAML: a `Label` with `x:Name="TitleLabel"` and a `Button` with `Clicked="OnAnimateClicked"`, inside a layout such as `VerticalStackLayout`.

## Properties

| Property | Type | Description | Default value |
|----------|------|-------------|---------------|
| Scale | `double` | The scale to animate to. | `1.2` |
| Length | `uint` | The duration of the whole animation: half out, half back, in milliseconds. | `340` |
| Easing | [Easing](xref:Microsoft.Maui.Easing) | The easing function applied to each part of the animation. | `Easing.Linear` |

Values for `double` properties must be finite numbers: `NaN` and infinity are ignored.

## Behavior

- Returns the view to its original scale when it ends.
- When triggered again while it runs, the new run continues from where the view is and ends at the original scale. The run it interrupts leaves the view to the new run.
- Cancelling the token mid-run returns the view to its original scale, then the awaited `Animate` throws `OperationCanceledException`. A token that is already cancelled throws before the view changes. Through `AnimationBehavior`, the command ends without an exception.
- When it is stopped and nothing takes over, for example by `CancelAnimations()` or another `AnimationBehavior` on the same view, the view returns to its original scale at once and `Animate` completes.
- With the system's animations off, also when they are switched off mid-run, the view ends at its original scale.

## Examples

You can find an example of this animation in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/AnimationBehaviorPage.xaml).

## API

You can find the source code for `ScaleAnimation` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Animations/ScaleAnimation.shared.cs).
