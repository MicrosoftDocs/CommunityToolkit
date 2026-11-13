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

The `FadeAnimation` can be used as follows in C#:

```csharp
public async Task Animate()
{
    var label = new Label();
    
    var fadeAnimation = new FadeAnimation
    {
        Opacity = 0.5
    };
    
    await fadeAnimation.Animate(label);
}
```

## Properties

| Property | Type | Description | Default value |
|----------|------|-------------|---------------|
| Opacity | `double` | The opacity to fade to before returning to the view's original opacity. | `0.3` |
| Length | `uint` | The duration of the whole animation, in milliseconds: half to fade out, half to fade back. | `300` |
| Easing | [Easing](xref:Microsoft.Maui.Easing) | The easing function applied to each part of the animation. | `Easing.Linear` |

> [!NOTE]
> `Length` is the duration of the whole animation: half of it to fade out and half to fade back. Previously the animation took twice `Length`. For more information, see [the discussion on GitHub](https://github.com/CommunityToolkit/Maui/discussions/1231).

## Behavior

- Returns the view to its original opacity when it ends.
- When triggered again while it runs, the new run continues from where the view is and ends at the original opacity. The run it interrupts stops where it is.
- Cancelling the token mid-run returns the view to its original opacity, then the awaited `Animate` throws `OperationCanceledException`. Previously `Animate` returned without an exception and left the view partly faded. A token that is already cancelled throws before the view changes. Through `AnimationBehavior` that exception is unhandled unless you call [`SetShouldSuppressExceptionsInAnimations(true)`](../options.md#setshouldsuppressexceptionsinanimations).

## Examples

You can find an example of this animation in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/AnimationBehaviorPage.xaml).

## API

You can find the source code for `FadeAnimation` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Animations/FadeAnimation.shared.cs).
