---
title: BounceAnimation - .NET MAUI Community Toolkit
author: TheCodeTraveler
description: The BounceAnimation hops a VisualElement up and down, with two smaller hops after the first.
ms.date: 11/13/2026
---

# BounceAnimation

The `BounceAnimation` hops a `VisualElement` up, lets it fall and then repeats with two smaller hops. The view slows down on the way up and speeds up on the way down.

## Syntax

### XAML

For use within XAML the `BounceAnimation` must be used in conjunction with the [`AnimationBehavior`](../behaviors/animation-behavior.md).

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the BounceAnimation

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
                    <toolkit:BounceAnimation Distance="50" />
                </toolkit:AnimationBehavior.AnimationType>
            </toolkit:AnimationBehavior>
        </Label.Behaviors>
    </Label>

</ContentPage>
```

### C#

The `BounceAnimation` can be used as follows in C#, here from a `Button.Clicked` handler:

```csharp
using CommunityToolkit.Maui.Animations;

public partial class MainPage : ContentPage
{
    public MainPage() => InitializeComponent();

    async void OnAnimateClicked(object? sender, EventArgs e)
    {
        var animation = new BounceAnimation
        {
            Distance = 50
        };

        await animation.Animate(TitleLabel);
    }
}
```

`TitleLabel` and `OnAnimateClicked` come from the page's XAML: a `Label` with `x:Name="TitleLabel"` and a `Button` with `Clicked="OnAnimateClicked"`, inside a layout such as `VerticalStackLayout`.

## Properties

| Property | Type | Description | Default value |
|----------|------|-------------|---------------|
| Distance | `double` | The height of the first hop, in device-independent units. A negative value bounces downward. | `30` |
| Length | `uint` | The time, in milliseconds, over which to animate. | `800` |
| Easing | [Easing](xref:Microsoft.Maui.Easing) | The easing function applied to the progress of the whole animation. See [Behavior](#behavior). | `Easing.Linear` |

Values for `double` properties must be finite numbers: `NaN` and infinity are ignored.

## Behavior

- Changes only `TranslationY`, relative to the view's own value, and returns it when it ends. The second hop is half and the third two-fifteenths of `Distance`.
- A view runs one [attention seeker](index.md#attention-seekers) at a time. Starting one, or triggering this one again, ends the running one and returns the view to rest first.
- Calling `Animate` does not stop a running `TranslateToAsync`, because that animation drives both axes in one handle. `AnimationBehavior` does stop it; see [AnimationBehavior](../behaviors/animation-behavior.md).
- Cancelling the token mid-run returns the view to rest, then the awaited `Animate` throws `OperationCanceledException`. A token that is already cancelled throws before the view changes. Through `AnimationBehavior`, the command ends without an exception.
- `Easing` warps the whole run, so use one that stays within 0..1 and only increases, such as `Linear`, `SinInOut` or `CubicOut`. `SpringOut` plays every keyframe early, then holds the view still until `Length` ends. `BounceOut` runs through the keyframes in about the first third of `Length`, then moves the view back and forth within the last keyframe. `SpringIn` holds the view still until late in the run. The view still ends at rest.

## Examples

You can find an example of this animation in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/AnimationBehaviorPage.xaml).

## API

You can find the source code for `BounceAnimation` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Animations/BounceAnimation.shared.cs).
