---
title: FadeAnimation - .NET MAUI Community Toolkit
author: bijington
description: The FadeAnimation provides the ability to animate the opacity of a VisualElement from its original opacity to a specified new opacity and then back to the original.
ms.date: 11/13/2026
---

# FadeAnimation

The `FadeAnimation` provides the ability to animate the opacity of a `VisualElement` from its original opacity to a specified new opacity and then back to the original.

## Syntax

### XAML

For use within XAML the `FadeAnimation` must be used in conjunction with the [`AnimationBehavior`](../behaviors/animation-behavior.md).

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the FadeAnimation

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
                    <toolkit:FadeAnimation Opacity="0.5" />
                </toolkit:AnimationBehavior.AnimationType>
            </toolkit:AnimationBehavior>
        </Label.Behaviors>
    </Label>

</ContentPage>
```

### C#

The `FadeAnimation` can be used as follows in C#, here from a `Button.Clicked` handler:

```csharp
using CommunityToolkit.Maui.Animations;

public partial class MainPage : ContentPage
{
    public MainPage() => InitializeComponent();

    async void OnAnimateClicked(object? sender, EventArgs e)
    {
        var fadeAnimation = new FadeAnimation
        {
            Opacity = 0.5
        };

        await fadeAnimation.Animate(TitleLabel);
    }
}
```

`TitleLabel` and `OnAnimateClicked` come from the page's XAML: a `Label` with `x:Name="TitleLabel"` and a `Button` with `Clicked="OnAnimateClicked"`, inside a layout such as `VerticalStackLayout`.

## Properties

| Property | Type | Description | Default value |
|----------|------|-------------|---------------|
| Opacity | `double` | The opacity to fade to before returning to the view's original opacity. | `0.3` |
| Length | `uint` | The duration of the whole animation, in milliseconds: half to fade out, half to fade back. | `300` |
| Easing | [Easing](xref:Microsoft.Maui.Easing) | The easing function applied to each part of the animation. | `Easing.Linear` |

> [!NOTE]
> `Length` now covers the whole animation. Previously the animation took twice `Length`. For more information, see [the discussion on GitHub](https://github.com/CommunityToolkit/Maui/discussions/1231).

> [!NOTE]
> `Opacity` now binds `OneWay` by default. It was `TwoWay`.

Values for `double` properties must be finite numbers: `NaN` and infinity are ignored.

## Behavior

- Returns the view to its original opacity when it ends.
- When triggered again while it runs, the new run continues from where the view is and ends at the original opacity. The run it interrupts leaves the view to the new run.
- Cancelling the token mid-run returns the view to its original opacity, then the awaited `Animate` throws `OperationCanceledException`. Previously `Animate` returned without an exception and left the view partly faded. A token that is already cancelled throws before the view changes. Through `AnimationBehavior`, the command ends without an exception.
- Stopped while nothing takes over, for example by `CancelAnimations()` or another `AnimationBehavior` on the same view, the view returns to its original opacity at once and `Animate` completes. Previously the view faded back over `Length`, or stayed partly faded when stopped on the way back.
- With the system's animations off, also when they are switched off mid-run, the view ends at its original opacity.

## Examples

You can find an example of this animation in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/AnimationBehaviorPage.xaml).

## API

You can find the source code for `FadeAnimation` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Animations/FadeAnimation.shared.cs).
