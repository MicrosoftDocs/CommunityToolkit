---
title: TouchBehavior - .NET MAUI Community Toolkit
author: bijington
description: The TouchBehavior is a Behavior that provides the ability to interact with any VisualElement based on touch, mouse click and hover events.
ms.date: 11/15/2026
---

# TouchBehavior

The `TouchBehavior` is a `Behavior` that provides the ability to interact with any `VisualElement` based on touch, mouse click and hover events. The `TouchBehavior` implementation makes it possible to customize many different visual properties of the `VisualElement` that it is attached to such as the background color, `Opacity`, `Rotation` and `Scale`, as well as many other properties.

> [!NOTE]
> The toolkit also provides the [`ImageTouchBehavior`](./image-touch-behavior.md) implementation that extends this `TouchBehavior` by also providing the ability to customize the `Source` of an `Image` element.

> [!IMPORTANT]
> **Breaking change after v17.0.0:** `DefaultBackgroundColor`, `HoveredBackgroundColor` and `PressedBackgroundColor` are painted as the element's `Background`. Through v17.0.0 they were written to `BackgroundColor`.
>
> - Why: on .NET MAUI 11.0.10 and later, that write removed a `DynamicResource` on `BackgroundColor` ([dotnet/maui#38063](https://github.com/dotnet/maui/pull/38063)).
> - Impact: a `VisualStateManager` or `Trigger` setter on `BackgroundColor` doesn't show while a state color is painted. Examples are a `CollectionView` item's `Selected` state and a `Button` style's `Disabled` state. The default and hovered states always paint a state color when `DefaultBackgroundColor` is set.
> - Reading: `BackgroundColor` no longer returns the state color. `Background` returns the behavior's brush while one shows.
> - See [Background colors](#background-colors) and [Migrate from v17.0.0](#migrate-from-v1700).

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

#### Using the TouchBehavior

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

The following example shows how to attach the `TouchBehavior` to a `HorizontalStackLayout` and change the background color and `Scale` of the `HorizontalStackLayout` when a user hovers their mouse cursor over the layout and any child elements.

```xaml
<HorizontalStackLayout
    Padding="20"
    BackgroundColor="Black"
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
    HorizontalOptions="Center"
    x:Name="TouchableHorizontalStackLayout">
    <HorizontalStackLayout.Behaviors>
        <toolkit:TouchBehavior
            BindingContext="{Binding Source={x:Reference Page}, Path=BindingContext, x:DataType=ContentPage}"
            LongPressDuration="750"
            LongPressCommand="{Binding Source={x:Reference Page}, Path=BindingContext.IncreaseLongPressCountCommand, x:DataType=ContentPage}"/>
    </HorizontalStackLayout.Behaviors>
</HorizontalStackLayout>
```

## Background colors

`DefaultBackgroundColor`, `HoveredBackgroundColor` and `PressedBackgroundColor` are painted as the element's `Background`. State colors are never written to `BackgroundColor`.

### How state colors are applied

- **Which color:**
  - Pressed uses `PressedBackgroundColor`, with no fallback.
  - Hovered uses `HoveredBackgroundColor`, else `DefaultBackgroundColor`.
  - Default uses `DefaultBackgroundColor`.
- **A state with a color:** the behavior sets its own `SolidColorBrush` as `Background` and animates it. Reading `Background` returns that brush.
- **A state without a color:** the brush animates to the element's `BackgroundColor`, then is removed.
- **`BackgroundColor` keeps your value:** bindings, `DynamicResource`, `AppThemeBinding` and `Style` keep working, except in the case under Exception below. A change made while a state color shows appears when the state ends.
- **The element's own `Background`:** an element with one shows no state colors. A `Background` you set while a state color shows replaces the behavior's brush and stays.
- **Setters:**
  - On `BackgroundColor`, they are hidden while a state color is painted.
  - On `Background`, they win while they apply. No state color shows then, pressed and hovered included.
- **`BackgroundColorTo`:** a state change no longer stops your animation. It runs hidden under the brush and shows once no state color is painted.
- **Detach:** removing the behavior or unloading the element (for example a recycled `CollectionView` item) removes the brush and stops the behavior's animation, so `BackgroundColor` shows again. Re-attaching repaints at once.
- **Exception:** an element with no `BackgroundColor` gets `Colors.Transparent` as its own value at the first state update after attach when that state has no color, and keeps it after detach. That value hides a binding, `Style` or `DynamicResource` on `BackgroundColor` that had no color yet.
- **Platforms:** the color logic is the same on every platform. On Android and Windows the behavior selects the tapped `CollectionView` item. On iOS and Mac Catalyst the platform does. The `Selected` visual state applies either way.

### Migrate from v17.0.0

Symptom: a `CollectionView` item root with `DefaultBackgroundColor` and a `Selected` setter on `BackgroundColor` loses its selection highlight. There is no build warning.

#### Fix 1 (recommended): move the resting color to `BackgroundColor`

Move the resting color from `DefaultBackgroundColor` to the element's `BackgroundColor`. Keep `PressedBackgroundColor` or `HoveredBackgroundColor`.

- `Selected` then shows, except while the item is pressed or hovered.
- When the press ends, the brush fades out and the `Selected` color shows.

Before:

```xaml
<toolkit:TouchBehavior DefaultBackgroundColor="White" PressedBackgroundColor="LightGray" />
```

After:

```xaml
<CollectionView ItemsSource="{Binding Items}" SelectionMode="Single">
    <CollectionView.ItemTemplate>
        <DataTemplate x:DataType="local:Item">
            <Grid Padding="12" BackgroundColor="White">
                <VisualStateManager.VisualStateGroups>
                    <VisualStateGroupList>
                        <VisualStateGroup Name="CommonStates">
                            <VisualState Name="Normal" />
                            <VisualState Name="Selected">
                                <VisualState.Setters>
                                    <Setter Property="BackgroundColor" Value="LightSkyBlue" />
                                </VisualState.Setters>
                            </VisualState>
                        </VisualStateGroup>
                    </VisualStateGroupList>
                </VisualStateManager.VisualStateGroups>
                <Grid.Behaviors>
                    <toolkit:TouchBehavior PressedBackgroundColor="LightGray" />
                </Grid.Behaviors>
                <Label Text="{Binding Name}" />
            </Grid>
        </DataTemplate>
    </CollectionView.ItemTemplate>
</CollectionView>
```

#### Fix 2: set `Background` in the `Selected` state

Keep `DefaultBackgroundColor` and change the `Selected` setter to `Property="Background"`. `Value="LightSkyBlue"` converts to a `SolidColorBrush`.

- `Selected` then wins over every state color, so no pressed or hovered color shows while the item is selected.
- Also set the element's `BackgroundColor` to the `DefaultBackgroundColor` value. Otherwise, after deselection the element can show its `BackgroundColor` until the next touch or hover repaints the state color.

```xaml
<Grid Padding="12" BackgroundColor="White">
    <VisualStateManager.VisualStateGroups>
        <VisualStateGroupList>
            <VisualStateGroup Name="CommonStates">
                <VisualState Name="Normal" />
                <VisualState Name="Selected">
                    <VisualState.Setters>
                        <Setter Property="Background" Value="LightSkyBlue" />
                    </VisualState.Setters>
                </VisualState>
            </VisualStateGroup>
        </VisualStateGroupList>
    </VisualStateManager.VisualStateGroups>
    <Grid.Behaviors>
        <toolkit:TouchBehavior DefaultBackgroundColor="White" PressedBackgroundColor="LightGray" />
    </Grid.Behaviors>
</Grid>
```

#### Button `Disabled` state

The same two fixes apply to a `Button` style's `Disabled` state: use `BackgroundColor` instead of `DefaultBackgroundColor`, or set `Background` in the `Disabled` state.

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
| DefaultBackgroundColor | `Color` | Gets or sets the background color of the element when the `CurrentTouchState` property is `TouchState.Default`, and when hovered without a `HoveredBackgroundColor`. Painted as the element's `Background`; `BackgroundColor` keeps its value. See [Background colors](#background-colors). |
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
| HoveredBackgroundColor | `Color` | Gets or sets the background color of the element when the `CurrentHoverState` property is `HoverState.Hovered`. `null` uses `DefaultBackgroundColor`. Painted as the element's `Background`; `BackgroundColor` keeps its value. See [Background colors](#background-colors). |
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
| PressedBackgroundColor | `Color` | Gets or sets the background color of the element when the `CurrentTouchState` property is `TouchState.Pressed`. `null` shows the element's own `BackgroundColor` while pressed; `DefaultBackgroundColor` isn't used. Painted as the element's `Background`; `BackgroundColor` keeps its value. See [Background colors](#background-colors). |
| PressedOpacity | `double` | Gets or sets the opacity of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedRotation | `double` | Gets or sets the rotation around both the X and Y axes of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedRotationX | `double` | Gets or sets the rotation around the X axis of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedRotationY | `double` | Gets or sets the rotation around the Y axis of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedScale | `double` | Gets or sets the scale of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedTranslationX | `double` | Gets or sets the X translation of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| PressedTranslationY | `double` | Gets or sets the Y translation of the element when the `CurrentTouchState` property is `TouchState.Pressed`. |
| ShouldMakeChildrenInputTransparent | `bool` | Gets or sets a value indicating whether the children of the element should be made input transparent. A change applies while the behavior is attached: `false` gives each child back the `InputTransparent` value it had. |

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

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/TouchBehavior/TouchBehaviorPage.xaml).

## API

You can find the source code for `TouchBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/PlatformBehaviors/Touch/TouchBehavior.shared.cs).


## Migrating From Xamarin Community Toolkit

In the [Xamarin Community Toolkit](https://github.com/xamarin/XamarinCommunityToolkit), there was the [`TouchEffect`](/dotnet/api/xamarin.communitytoolkit.effects.toucheffect?view=xamarin-community-toolkit-sdk&preserve-view=true) if you are upgrading an app from Xamarin.Forms to .NET MAUI there are some breaking changes that you should be aware of:

1. [API Name Changes](#api-name-changes)
2. [TouchBehavior is now implemented as a `PlatformBehavior`](#touchbehavior-is-now-implemented-as-a-platformbehavior)

### API Name Changes

| Name In Xamarin Community Toolkit | Name In MAUI Community Toolkit                       |
|-----------------------------------|------------------------------------------------------|
| TouchEffect                       | TouchBehavior                                        |
| NormalBackgroundColor             | DefaultBackgroundColor                               |
| NormalScale                       | DefaultScale                                         |
| NormalOpacity                     | DefaultOpacity                                       |
| NormalTranslationX                | DefaultTranslationX                                  |
| NormalTranslationY                | DefaultTranslationY                                  |
| NormalRotation                    | DefaultRotation                                      |
| NormalRotationX                   | DefaultRotationX                                     |
| NormalRotationY                   | DefaultRotationY                                     |
| NormalAnimationDuration           | DefaultAnimationDuration                             |
| NormalAnimationEasing             | DefaultAnimationEasing                               |
| NormalBackgroundImageSource       | DefaultImageSource (Moved to `ImageTouchBehavior`)   |
| NormalBackgroundImageAspect       | DefaultImageAspect (Moved to  `ImageTouchBehavior` ) |

### TouchBehavior is now implemented as a `PlatformBehavior`

In the Xamarin Community Toolkit the `TouchEffect` was implemented as an `AttachedEffect`. To use the effect you would use the attached properties and apply to any `VisualElement`

In .NET MAUI the `TouchBehavior` is implemented as a `PlatformBehavior` which is now applied to the elements behavior collection, see [Platform Behaviors](/dotnet/maui/fundamentals/behaviors#platform-behaviors) for more information.

> Note: By default in .NET MAUI `PlatformBehavior`s will not set the `BindingContext` property, this is because Behaviors can be shared in styles. The `TouchBehavior` will set the `BindingContext` property equal to the `VisualElement` it is applied to. This means that you should _not_ share the `TouchBehavior` between elements via styles.

Below is an example of a `TouchEffect` being applied to a view in Xamarin.Forms:

<!-- markdownlint-disable MD025 -->
#### [XAML](#tab/toucheffect-xaml)

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

#### [C#](#tab/toucheffect-csharp)

```csharp
var stackLayout = new StackLayout()
{
    HorizontalOptions = LayoutOptions.CenterAndExpand,
    Orientation = StackOrientation.Horizontal,
    Children =
    {
        new BoxView() { Color = Color.Gold, },
        new Label() { Text = "The entire layout receives touches", },
        new BoxView() { Color = Color.Gold, },
    }
};

TouchEffect.SetAnimationDuration(stackLayout, 250);
TouchEffect.SetAnimationEasing(stackLayout, Easing.CubicInOut);
TouchEffect.SetPressedScale(stackLayout, 0.8);
TouchEffect.SetPressedOpacity(stackLayout, 0.6);
TouchEffect.SetCommand(stackLayout, command);
```

__ _

The equivalent `TouchBehavior` in .NET MAUI would look like this:

<!-- markdownlint-disable MD025 -->
#### [XAML](#tab/touchbehavior-xaml)

```xaml
<HorizontalStackLayout 
    HorizontalOptions="Center" 
    VerticalOptions="Center"
    x:Name="TouchableHorizontalLayout">
    <HorizontalStackLayout.Behaviors>
        <toolkit:TouchBehavior
            DefaultAnimationDuration="250"
            DefaultAnimationEasing="{x:Static Easing.CubicInOut}"
            PressedOpacity="0.6"
            PressedScale="0.8"
            BindingContext="{Binding Path=BindingContext, Source={x:Reference TouchableHorizontalLayout}, x:DataType=HorizontalStackLayout}"
            Command="{Binding LayoutTappedCommand}" />
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

#### [C#](#tab/touchbehavior-csharp)

```csharp
var stackLayout = new HorizontalStackLayout()
{
    HorizontalOptions = LayoutOptions.Center,
    VerticalOptions = LayoutOptions.Center,
    Children =
    {
        new ContentView()
        {
            BackgroundColor = Colors.Gold,
            HeightRequest = 100,
            WidthRequest = 10,
        },
        new Label()
        {
            LineBreakMode = LineBreakMode.TailTruncation,
            Text = "The entire layout receives touches",
            VerticalOptions = LayoutOptions.Center,
        },
        new ContentView()
        {
            BackgroundColor = Colors.Gold,
            HeightRequest = 100,
            WidthRequest = 10,
        },
    },
    Behaviors =
    {
        new TouchBehavior()
        {
            DefaultAnimationDuration = 250,
            DefaultAnimationEasing = Easing.CubicInOut,
            PressedOpacity = 0.6,
            PressedScale = 0.8,
            Command = command,
            BindingContext = this.BindingContext
        }
    }
};
```
