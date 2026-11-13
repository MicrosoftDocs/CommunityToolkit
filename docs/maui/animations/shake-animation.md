---
title: ShakeAnimation - .NET MAUI Community Toolkit
author: bijington
description: The ShakeAnimation shakes a VisualElement sideways around its original position, with each swing smaller than the last.
ms.date: 11/13/2026
---

# ShakeAnimation

The `ShakeAnimation` shakes a `VisualElement` sideways around its original position. The first swing moves the view `StartFactor` units either way and each following swing is `ReducingAmount` smaller, until the view is back at rest.

## Syntax

### XAML

For use within XAML the `ShakeAnimation` must be used in conjunction with the [`AnimationBehavior`](../behaviors/animation-behavior.md).

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ShakeAnimation

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
                    <toolkit:ShakeAnimation StartFactor="20" ReducingAmount="4" />
                </toolkit:AnimationBehavior.AnimationType>
            </toolkit:AnimationBehavior>
        </Label.Behaviors>
    </Label>

</ContentPage>
```

### C#

The `ShakeAnimation` can be used as follows in C#:

```csharp
public async Task Animate()
{
    var label = new Label();

    var animation = new ShakeAnimation
    {
        StartFactor = 20,
        ReducingAmount = 4
    };

    await animation.Animate(label);
}
```

## Properties

| Property | Type | Description | Default value |
|----------|------|-------------|---------------|
| StartFactor | `double` | The biggest movement of the shake, in device-independent units. | `15` |
| ReducingAmount | `double` | The amount each swing is smaller than the previous one. It must be a finite number greater than 0, otherwise `Animate` throws an `ArgumentOutOfRangeException`; `NaN` and infinity are ignored. | `5` |
| Length | `uint` | The time, in milliseconds, over which to animate. | `300` |
| Easing | [Easing](xref:Microsoft.Maui.Easing) | The easing function applied to each movement of the shake. | `Easing.Linear` |

Values for `double` properties must be finite numbers: `NaN` and infinity are ignored.

## Behavior

- Changes only `TranslationX`, around the view's own value, and returns it when it ends.
- A view runs one [attention seeker](index.md) at a time. Starting one, or triggering this one again, ends the running one and returns the view to rest first.
- Cancelling the token mid-run returns the view to rest, then the awaited `Animate` throws `OperationCanceledException`. A token that is already cancelled throws before the view changes. Through `AnimationBehavior` that exception is unhandled unless you call [`SetShouldSuppressExceptionsInAnimations(true)`](../options.md#setshouldsuppressexceptionsinanimations).
- `Easing` shapes each movement on a linear timeline, so an overshooting easing only overshoots that one swing.
- The shake has at most 100 swings; after the 100th the view moves straight back to rest.

## Examples

You can find an example of this animation in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/AnimationBehaviorPage.xaml).

## API

You can find the source code for `ShakeAnimation` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Animations/ShakeAnimation.shared.cs).
