---
title: TouchBehavior - .NET MAUI Community Toolkit
author: bijington
description: The TouchBehavior is a Behavior that provides the ability to interact with any VisualElement based on touch, mouse click and hover events.
ms.date: 03/25/2024
---

# TouchBehavior

The `TouchBehavior` is a `Behavior` that provides the ability to interact with any `VisualElement` based on touch, mouse click and hover events. The `TouchBehavior` implementation makes it possible to customize many different visual properties of the `VisualElement` that it is attached to such as the `BackgroundColor`, `Opacity`, `Rotation` and `Scale`, as well as many other properties.

> [!NOTE]
> The toolkit also provides the [`ImageTouchBehavior`](./image-touch-behavior.md) implementation that extends this `TouchBehavior` by also providing the ability to customize the `Source` of an `Image` element.

## Syntax

The following examples show how to add the `TouchBehavior` to a parent `HorizontalStackLayout` and perform the following animations when a user touches or clicks on the `HorizontalStackLayout` or any of its children:

- animates over a period of 250 milliseconds
- applies the `CubicInOut` [`Easing`](/dotnet/maui/user-interface/animation/easing)
- changes the `Opacity` to 0.6
- changes the `Scale` to 0.8

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the AnimationBehavior

```xaml
<ContentPage 
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
    x:Class="CommunityToolkit.Maui.Sample.Pages.Behaviors.TouchBehaviorPage">

   <HorizontalStackLayout HorizontalOptions="CenterAndExpand" VerticalOptions="Center">
        <HorizontalStackLayout.Behaviors>
            <toolkit:TouchBehavior
                DefaultAnimationDuration="250"
                DefaultAnimationEasing="{x:Static Easing.CubicInOut}"
                PressedOpacity="0.6"
                PressedScale="0.8" />
        </HorizontalStackLayout.Behaviors>

        <ContentView
            HeightRequest="100"
            WidthRequest="10"
            BackgroundColor="Gold" />
        <Label Text="The entire layout receives touches" VerticalOptions="Center" LineBreakMode="TailTruncation"/>
        <ContentView
            HeightRequest="100"
            WidthRequest="10"
            BackgroundColor="Gold" />
    </HorizontalStackLayout>

</ContentPage>
```

### C#

The `TouchBehavior` can be used as follows in C#:

```csharp
class TouchBehaviorPage : ContentPage
{
    public TouchBehaviorPage()
    {
        var firstContent = new ContentView
        {
            HeightRequest = 100,
            WidthRequest = 10,
            BackgroundColor = Colors.Gold
        };

        var label = new Label
        {
            Text = "The entire layout receives touches",
            VerticalOptions = LayoutOptions.Center,
            LineBreakMode = LineBreakMode.TailTruncation
        };

        var secondContent = new ContentView
        {
            HeightRequest = 100,
            WidthRequest = 10,
            BackgroundColor = Colors.Gold
        };

        var layout = new HorizontalStackLayout
        {
            HorizontalOptions = LayoutOptions.CenterAndExpand,
            VerticalOptions = LayoutOptions.Center,
            Children = 
            {
                firstContent,
                label,
                secondContent
            }
        }

        var touchBehavior = new TouchBehavior
        {
            DefaultAnimationDuration = 250,
            DefaultAnimationEasing = Easing.CubicInOut,
            PressedOpacity = 0.6,
            PressedScale = 0.8
        };

        layout.Behaviors.Add(touchBehavior);

        Content = layout;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class TouchBehaviorPage : ContentPage
{
    public TouchBehaviorPage()
    {
        Content = new HorizontalStackLayout
        {
            HorizontalOptions = LayoutOptions.CenterAndExpand,
            VerticalOptions = LayoutOptions.Center,
            Children = 
            {
                new ContentView()
                    .Size(10, 100)
                    .BackgroundColor(Colors.Gold),

                new Label
                {
                    LineBreakMode = LineBreakMode.TailTruncation
                }
                    .Text("The entire layout receives touches"
                    .CenterVertical(),

                new ContentView()
                    .Size(10, 100)
                    .BackgroundColor(Colors.Gold)
            }
        }
            .Behaviors(new TouchBehavior
            {
                DefaultAnimationDuration = 250,
                DefaultAnimationEasing = Easing.CubicInOut,
                PressedOpacity = 0.6,
                PressedScale = 0.8
            });
    }
}
```

## Additional examples

### Handling hover interaction

The `TouchBehavior` provides the ability to customize the properties of the attached `VisualElement` based on whether the mouse it hovering over the element.

The following example shows how to attach the `TouchBehavior` to a `HorizontalStackLayout` and change the `BackgroundColor` and `Scale` of the `HorizontalStackLayout` when a user hovers their mouse cursor over the layout and any child elements.

```xaml
<HorizontalStackLayout
    Padding="20"
    Background="Black"
    HorizontalOptions="CenterAndExpand">
    <HorizontalStackLayout.Behaviors>
        <toolkit:TouchBehavior
            HoveredBackgroundColor="{StaticResource Gray900}"
            HoveredScale="1.2" />
    </HorizontalStackLayout.Behaviors>
</HorizontalStackLayout>
```

### Handling long press interaction

The `TouchBehavior` provides the ability to handle the scenario when a user presses for a long period of time. This period of time can be defined by the `LongPressDuration` which is in units of milliseconds.

The following example shows how to add the `TouchBehavior` to a `HorizontalStackLayout`, bind the `LongPressCommand` to the `IncreaseLongPressCountCommand` defined in the backing view model and set the `LongPressDuration` to 750 milliseconds.

#### View

```xaml
<HorizontalStackLayout
    Padding="20"
    Background="Black"
    HorizontalOptions="CenterAndExpand">
    <HorizontalStackLayout.Behaviors>
        <toolkit:TouchBehavior
            LongPressDuration="750"
            LongPressCommand="{Binding Source={x:Reference Page}, Path=BindingContext.IncreaseLongPressCountCommand}"/>
    </HorizontalStackLayout.Behaviors>
</HorizontalStackLayout>
```

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/TouchBehaviorPage.xaml).

## API

You can find the source code for `TouchBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/TouchnBehavior.shared.cs).
