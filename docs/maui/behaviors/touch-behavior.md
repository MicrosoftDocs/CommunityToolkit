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

[!INCLUDE [important note on bindings within behaviors](../includes/behavior-bindings.md)]

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

   <HorizontalStackLayout HorizontalOptions="Center" VerticalOptions="Center">
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
            HorizontalOptions = LayoutOptions.Center,
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
            HorizontalOptions = LayoutOptions.Center,
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
    HorizontalOptions="Center">
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

```xaml
<HorizontalStackLayout
    Padding="20"
    Background="Black"
    HorizontalOptions="Center">
    <HorizontalStackLayout.Behaviors>
        <toolkit:TouchBehavior
            LongPressDuration="750"
            LongPressCommand="{Binding Source={x:Reference Page}, Path=BindingContext.IncreaseLongPressCountCommand}"/>
    </HorizontalStackLayout.Behaviors>
</HorizontalStackLayout>
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| Command | `ICommand` | Gets or sets the `ICommand` to invoke when the user has completed a touch gesture. |
| CommandParameter | `object` | Gets or sets the parameter to pass to the `Command` property. |
| CurrentHoverState | `HoverState` | Gets or sets the current `HoverState` of the behavior. |
| CurrentHoverStatus | `HoverStatus` | Gets or sets the current `HoverStatus` of the behavior. |
| CurrentInteractionStatus | `TouchInteractionStatus` | Gets or sets the current `TouchInteractionStatus` of the behavior. |
| CurrentTouchState | `TouchState` | Gets or sets the current `TouchState` of the behavior. |
| CurrentTouchStatus | `TouchStatus` | Gets or sets the current `TouchStatus` of the behavior. |
| DefaultAnimationDuration | `int` | Gets or sets the duration of the animation when the `CurrentTouchState` property is `TouchState.Default`. |
| DefaultAnimationEasing | `Easing` | Gets or sets the easing of the animation when the `CurrentTouchState` property is `TouchState.Default`. |
| DefaultBackgroundColor | `Color` | Gets or sets the background color of the element when the `CurrentTouchState` property is `TouchState.Default`. |
| DefaultOpacity | `double` | Gets or sets the opacity of the element when the `CurrentTouchState` property is `TouchState.Default`. |
| DefaultRotation | `double` | Gets or sets the rotation around both the X and Y axes of the element when the `CurrentTouchState` property is `TouchState.Default`. |
| DefaultRotationX | `double` | Gets or sets the rotation around the X axis of the element when the `CurrentTouchState` property is `TouchState.Default`. |
| DefaultRotationY | `double` | Gets or sets the rotation around the Y axis of the element when the `CurrentTouchState` property is `TouchState.Default`. |
| DefaultScale | `double` | Gets or sets the scale of the element when the `CurrentTouchState` property is `TouchState.Default`. |
| DefaultTranslationX | `double` | Gets or sets the X translation of the element when the `CurrentTouchState` property is `TouchState.Default`. |
| DefaultTranslationY | `double` | Gets or sets the Y translation of the element when the `CurrentTouchState` property is `TouchState.Default`. |
| DisallowTouchThreshold | `int` | Gets or sets the threshold for disallowing touch. |
| HoveredAnimationDuration | `int` | Gets or sets the duration of the animation when the `CurrentHoverState` property is `HoverState.Hovered`. |
| HoveredAnimationEasing | `Easing` | Gets or sets the easing of the animation when the `CurrentHoverState` property is `HoverState.Hovered`. |
| HoveredBackgroundColor | `Color` | Gets or sets the background color of the element when the `CurrentHoverState` property is `HoverState.Hovered`. |
| HoveredOpacity | `double` | Gets or sets the opacity of the element when the `CurrentHoverState` property is `HoverState.Hovered`. |
| HoveredRotation | `double` | Gets or sets the rotation around both the X and Y axes of the element when the `CurrentHoverState` property is `HoverState.Hovered`. |
| HoveredRotationX | `double` | Gets or sets the rotation around the X axis of the element when the `CurrentHoverState` property is `HoverState.Hovered`. |
| HoveredRotationY | `double` | Gets or sets the rotation around the Y axis of the element when the `CurrentHoverState` property is `HoverState.Hovered`. |
| HoveredScale | `double` | Gets or sets the scale of the element when the `CurrentHoverState` property is `HoverState.Hovered`. |
| HoveredTranslationX | `double` | Gets or sets the X translation of the element when the `CurrentHoverState` property is `HoverState.Hovered`. |
| HoveredTranslationY | `double` | Gets or sets the Y translation of the element when the `CurrentHoverState` property is `HoverState.Hovered`. |
| IsEnabled | `bool` | Gets or sets a value indicating whether the behavior is enabled. |
| LongPressCommand | `ICommand` | Gets or sets the `ICommand` to invoke when the user has completed a long press. |
| LongPressCommandParameter | `object` | Gets or sets the parameter to pass to the `LongPressCommand` property. |
| LongPressDuration | `int` | Gets or sets the duration in milliseconds required to trigger the long press gesture. |
| PressedAnimationDuration | `int` | Gets or sets the duration of the animation when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedAnimationEasing | `Easing` | Gets or sets the easing of the animation when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedBackgroundColor | `Color` | Gets or sets the background color of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedOpacity | `double` | Gets or sets the opacity of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedRotation | `double` | Gets or sets the rotation around both the X and Y axes of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedRotationX | `double` | Gets or sets the rotation around the X axis of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedRotationY | `double` | Gets or sets the rotation around the Y axis of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedScale | `double` | Gets or sets the scale of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedTranslationX | `double` | Gets or sets the X translation of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedTranslationY | `double` | Gets or sets the Y translation of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| ShouldMakeChildrenInputTransparent | `bool` | Gets or sets a value indicating whether the children of the element should be made input transparent. |

## Events

|Event | Description  |
|---------|---------|
| `CurrentTouchStateChanged` | Fires when `CurrentTouchState` changes. |
| `CurrentTouchStatusChanged` | Fires when `CurrentTouchStatus` changes. |
| `HoverStateChanged` | Fires when `CurrentHoverState` changes. |
| `HoverStatusChanged` | Fires when `CurrentHoverStatus` changes. |
| `InteractionStatusChanged` | Fires when `CurrentInteractionStatus` changes. |
| `LongPressCompleted` | Fires when a long press gesture has completed. |
| `TouchGestureCompleted` | Fires when a touch gesture has completed. |

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/TouchBehaviorPage.xaml).

## API

You can find the source code for `TouchBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/TouchBehavior.shared.cs).


## Migrating From Xamarin Community Toolkit

In the [Xamarin Community Toolkit](https://github.com/xamarin/XamarinCommunityToolkit), there was the [`TouchEffect`](/dotnet/api/xamarin.communitytoolkit.effects.toucheffect?view=xamarin-community-toolkit-sdk) if you are upgrading an app from Xamarin.Forms to .NET Maui there are a number of changes that you need to be aware of:

1. [`TouchBehavior` is now a `PlatformBehavior`](#TouchBehavior-is-now-a-PlatformBehavior)
2. [The `BindingContext` is not automatically set](#Setting-The-TouchBehavior-Binding-Context)

### TouchBehavior is now a PlatformBehavior

In the Xamarin Community Toolkit the `TouchEffect` was implemented as an `AttachedEffect`. To use the effect you would use the attached properties and apply to any `VisualElement`

In .NET Maui the `TouchBehavior` is implemented as a `PlatformBehavior` behavior is now applied to the elements behavior collection, see [Platform Behaviors](/dotnet/maui/fundamentals/behaviors#platform-behaviors) for more information.

Below is an example of a `TouchEffect` being applied to a view in Xamarin Forms:

```xaml
<StackLayout Orientation="Horizontal"
            HorizontalOptions="CenterAndExpand"
            xct:TouchEffect.AnimationDuration="250"
            xct:TouchEffect.AnimationEasing="{x:Static Easing.CubicInOut}"
            xct:TouchEffect.PressedScale="0.8"
            xct:TouchEffect.PressedOpacity="0.6"
            xct:TouchEffect.Command="{Binding Command}">
    <BoxView Color="Gold" />
    <Label Text="The entire layout receives touches" />
    <BoxView Color="Gold"/>
</StackLayout>
```

The equivalent `TouchBehavior` in .NET Maui would look like this:

```xaml
<HorizontalStackLayout HorizontalOptions="CenterAndExpand" VerticalOptions="Center">
    <HorizontalStackLayout.Behaviors>
        <mct:TouchBehavior
            DefaultAnimationDuration="250"
            DefaultAnimationEasing="{x:Static Easing.CubicInOut}"
            PressedOpacity="0.6"
            PressedScale="0.8" />
    </HorizontalStackLayout.Behaviors>

    <ContentView
        BackgroundColor="Gold"
        HeightRequest="100"
        WidthRequest="10" />
    <Label
        LineBreakMode="TailTruncation"
        Text="The entire layout receives touches"
        VerticalOptions="Center" />
    <ContentView
        BackgroundColor="Gold"
        HeightRequest="100"
        WidthRequest="10" />
</HorizontalStackLayout>
```

### Setting The TouchBehavior Binding Context

As noted in the previous section, the `BindingContext` of the behavior is not set automatically, the reason for this is outlined in the Maui documentation for [Behaviors](/dotnet/maui/fundamentals/behaviors#create-a-net-maui-behavior):

> .NET MAUI does not set the BindingContext of a behavior, because behaviors can be shared and applied to multiple controls through styles.

You should note that whilst .NET Maui behaviors can be shared via styles, the `TouchBehavior` is inteded to be applied to a specific `VisualElement` and should not be shared across multiple views. A new instance of the `TouchBehavior` should be created for every `VisualElement` it is applied to.

Since the `TouchBehavior` does not inherit any `BindingContext`, the use of [Relative bindings](/dotnet/maui/fundamentals/data-binding/relative-bindings) is unsupported since the behavior has no way of obtaining any information about the `BindingContext` of the `VisualElement` it is applied to. Instead you should use an element in your view as an anchor to provide the `BindingContext` for the `TouchBehavior` using an `x:Reference`.

You can set an `x:Name` on any element on page to set the `BindingContext` of the `TouchBehavior` to your respective viewmodel. A convenient way of doing this is setting this at the root element of your view, for example the `ContentPage`.

```xaml
<ContentPage x:Name="Page">
    <HorizontalStackLayout HorizontalOptions="CenterAndExpand" VerticalOptions="Center">
        <HorizontalStackLayout.Behaviors>
            <mct:TouchBehavior
                BindingContext="{Binding Source={x:Reference Page}, Path=BindingContext}"
                Command="{Binding IncreaseTouchCountCommand}"
                DefaultAnimationDuration="250"
                DefaultAnimationEasing="{x:Static Easing.CubicInOut}"
                PressedOpacity="0.6"
                PressedScale="0.8" />
        </HorizontalStackLayout.Behaviors>

        <ContentView
            BackgroundColor="Gold"
            HeightRequest="100"
            WidthRequest="10" />
        <Label
            LineBreakMode="TailTruncation"
            Text="The entire layout receives touches"
            VerticalOptions="Center" />
        <ContentView
            BackgroundColor="Gold"
            HeightRequest="100"
            WidthRequest="10" />
    </HorizontalStackLayout>
</ContentPage>
```

If you are using a templated view, such as a `DataTemplate` you should use the parent view instead:

```xaml
<DataTemplate x:DataType="models:User">
    <ContentView x:Name="ContentView">
        <ContentView.Behaviors>
            <mct:TouchBehavior BindingContext="{Binding Source={x:Reference ContentView}, Path=BindingContext}"/>
        </ContentView.Behaviors>
        <Grid ColumnDefinitions="Auto, *">
        
            <Image Source="{Binding ProfilePicture}">

            <Label Text="{Binding UserName}" Grid.Column="1">
        </Grid>
    </ContentView>
</DataTemplate>
```