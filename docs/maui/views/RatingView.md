---
title: RatingView - .NET MAUI Community Toolkit
author: GeorgeLeithead
description: "The RatingView is designed to provide developers with a flexible and customizable rating mechanism, similar to those used on popular review and feedback platforms."
ms.date: 09/19/2024
---

# RatingView

The .NET MAUI Community Toolkit `RatingView` is a control designed to provide developers with a flexible and customizable rating mechanism, similar to those used on popular review and feedback platforms.


## Syntax

### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

### Using the RatingView

The following example shows how to create a `RatingView`:

![Screenshot of an RatingView example](../images/views/RatingView.png "RatingView example")

```xaml
<ContentPage
	x:Class="CommunityToolkit.Maui.Sample.Pages.MyPage"
	xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
	xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
	xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
	<VerticalStackLayout>
		<toolkit:RatingView
			EmptyColor="White"
			FilledColor="Blue"
			IsReadOnly="False"
			ItemPadding="3,7,7,3"
			ItemShapeSize="37"
			MaximumRating="5"
			RatingFill="Shape"
			Rating="4.5"
			Shape="Star"
			ShapeBorderColor="Red"
			ShapeBorderThickness="1"
			Spacing="3" />
	</VerticalStackLayout>
</ContentPage>
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

partial class MyPage : ContentPage
{
	public MyPage()
	{
		RatingView ratingView = new()
		{
			EmptyColor = Colors.White,
			FilledColor = Colors.Blue,
			IsReadOnly = false,
			ItemPadding = new Thickness(3,7,7,3),
			ItemShapeSize = 37,
			MaximumRating = 5,
			RatingFill = RatingFillElement.Shape,
			Rating = 4.5,
			Shape = RatingViewShape.Star,
			ShapeBorderColor = Colors.Red,
			ShapeBorderThickness = 1,
			Spacing = 3,
		};

		Content = ratingView;
	}
}
```

## Properties

| Property | Type | Description |
|---|---|---|
| AnchorX | `double` | Gets or sets the X component of the center point for any transform operation, relative to the bounds of the element. This is a bindable property. |
| AnchorY | `double` | Gets or sets the Y component of the center point for any transform operation, relative to the bounds of the element. This is a bindable property. |
| AutomationId | `string` | Gets or sets a value that allows the automation framework to find and interact with this element. |
| Background | `brush` | Gets or sets the Brush which will be used to fill the background of an element. This is a bindable property. |
| BackgroundColor | `color` | Gets or sets the Color which will fill the background of an element. This is a bindable property. |
| Batched | `bool` | Gets a value that indicates there are batched changes done for this element. |
| Behaviors	| `IList<Behavior>` | Gets the list of Behavior objects associated to this element. This is a read-only bindable property. |
| BindingContext | `object` | Gets or sets an object that contains the properties that will be targeted by the bound properties that belong to this BindableObject. This is a bindable property. |
| Bounds | `Microsoft.Maui.Graphics.Rect` | Gets the bounds of the element in device-independent units. |
| CascadeInputTransparent | `bool` | Gets or sets a value that controls whether child elements inherit the input transparency of this layout when the tranparency is true. |
| Children | `object` | Gets the child objects contained in this layout. |
| class | `IList<string>` | Gets or sets the style classes for the element. |
| ClassId | `string` | Gets or sets a value used to identify a collection of semantically similar elements. |
| Clip | `Shapes.Geometry` | Specifies the clipping region for an element. This is a bindable property. |
| Count | `int` | Gets the child object count in this layout. |
| CustomShape | `string` | Gets or sets the `Path` for rating item shapes. Only when the `Shape` property is set to `Custom` is the `CustomShape` be used. This is a bindable property. |
| DesiredSize | `Microsoft.Maui.Graphics.Size` | Gets the size that this element computed during the measure pass of the layout process. |
| DisableLayout | `bool` | Gets a value that indicates that layout for this element is disabled. |
| Dispatcher | `Microsoft.Maui.Dispatching.IDispatcher` | Gets the dispatcher that was available when this bindable object was created, otherwise tries to find the nearest available dispatcher (probably the window's/app's). |
| EffectControlProvider | `IEffectControlProvider` | For internal use by .NET MAUI. |
| Effects | `IList<Effect>` | Gets or sets the styles and properties that will be applied to the element during runtime. |
| EmptyColor | `Color` | Gets or sets the color that is applied to the unfilled (empty) rating items.  The default value is Transparent.  This is a bindable property. |
| FilledColor | `Color` | Gets or sets the Color that is applied to the filled (rated) portion of each rating item.  The default value is Yellow. This is a bindable property. |
| FlowDirection | `Microsoft.Maui.FlowDirection` | Gets or sets the layout flow direction. This is a bindable property. |
| Frame | `Microsoft.Maui.Graphics.Rect` | Gets or sets the frame this element resides in on screen. |
| GestureRecognizers | `IList<IGestureRecognizer>` | The collection of gesture recognizers associated with this view. |
| Handler | `Microsoft.Maui.IViewHandler?` | Gets or sets the IViewHandler associated to this element. |
| Height | `double` | Gets the current rendered height of this element. This is a read-only bindable property. |
| HeightRequest | `double` | Gets or sets the desired height override of this element. This is a bindable property. |
| HorizontalOptions | `LayoutOptions` | Gets or sets the LayoutOptions that define how the element gets laid out in a layout cycle. This is a bindable property. |
| Id | `Guid` | Gets a value that can be used to uniquely identify an element throughout the run of your application. |
| IgnoreSafeArea | `bool` | Specifies how the View's content should be positioned in relation to obstructions. If this value is false, the content will be positioned only in the unobstructed portion of the screen. If this value is true, the content may be positioned anywhere on the screen. This includes the portion of the screen behind toolbars, screen cutouts, etc. |
| InputTransparent | `bool` | Gets or sets a value indicating whether this element responds to hit testing during user interaction. This is a bindable property. |
| IsClippedToBounds | `bool` | Gets or sets a value which determines if the layout should clip its children to its bounds. The default value is false. |
| IsEnabled | `bool` | Gets or sets a value indicating whether this element is enabled in the user interface. This is a bindable property. |
| IsEnabledCore | `bool` | This value represents the cumulative IsEnabled value. All types that override this property need to also invoke the RefreshIsEnabledProperty() method if the value will change. |
| IsFocused | `bool` | Gets a value indicating whether this element is focused currently. This is a bindable property. |
| IsInPlatformLayout | `bool` | Gets or sets a value that indicates that this element is currently going through the platform layout cycle. |
| IsLoaded | `bool` | Indicates if an element is connected to the main object tree. |
| IsPlatformEnabled | `bool` | Gets or sets a value that indicates whether this elements's platform equivalent element is enabled. |
| IsPlatformStateConsistent | `bool` | Gets or sets a value that indicates that this element is currently consistent with the platform equivalent element state. |
| IsReadOnly | `bool` | Gets whether this layout is readonly. The default value is false.  This is a bindable property. |
| IsVisible | `bool` | Gets or sets a value that determines whether this element will be visible on screen and take up space in layouts. This is a bindable property. |
| ItemPadding | `Thickness` | Gets or sets the inner padding of the rating item. The default value is a Thickness with all values set to 0.  This is a bindable property. |
| Margin | `Thickness` | Gets or set the margin for the view. |
| MaximumHeightRequest | `double` | Gets or sets the maximum height the element will request during layout. This is a bindable property. |
| MaximumRating | `byte` | Gets or sets the maximum number of ratings. The range of this value is 1 to 25; values outside this range will be set to the nearest valid value.  The default value is 5. This is a bindable property. |
| MaximumWidthRequest | `double` | Gets or sets the maximum width the element will request during layout. This is a bindable property. |
| MinimumHeightRequest | `double` | Gets or sets the minimum height the element will request during layout. This is a bindable property. |
| MinimumWidthRequest | `double` | Gets or sets the minimum width the element will request during layout. This is a bindable property. |
| Navigation | `INavigation` | Gets the object responsible for handling stack-based navigation. |
| NavigationProxy | `Internals.NavigationProxy` | Gets the cast of Navigation to a NavigationProxy. |
| Opacity | `double` | Gets or sets the opacity value applied to the element when it is rendered. The range of this value is 0 to 1; values outside this range will be set to the nearest valid value. This is a bindable property. |
| Padding | `Thickness` | Gets or sets the inner padding of the layout. The default value is a Thickness with all values set to 0. |
| Parent | `Element` | Gets or sets the parent Element of this element. |
| RatingChanged | `EventHandler<RatingChangedEventArgs>` | Event occurs when the rating is changed. |
| RatingFill | `RatingFillElement` | Gets or sets a value indicating how the fill is applied against the entire rating item or just the shape. The property is of type [`RatingFillElement`](#set-rating-fill) and is an enumeration. The default value of this property is Shape.  This is a bindable property. |
| Rating | `double` | Gets or sets a value indicating the current rating value, allowing for both pre-defined ratings (e.g., from previous user input or stored data) and updates during runtime as the user interacts with the control.  The default value is 0.  This is a bindable property. |
| RealParent | `Element` | For internal use by .NET MAUI. |
| Resources | `ResourceDictionary` | Gets or sets the local resource dictionary. |
| Rotation | `double` | Gets or sets the rotation (in degrees) about the Z-axis (affine rotation) when the element is rendered. This is a bindable property. |
| RotationX | `double` | Gets or sets the rotation (in degrees) about the X-axis (perspective rotation) when the element is rendered. This is a bindable property. |
| RotationY | `double` | Gets or sets the rotation (in degrees) about the Y-axis (perspective rotation) when the element is rendered. This is a bindable property. |
| Scale | `double` | Gets or sets the scale factor applied to the element. This is a bindable property. |
| ScaleX | `double` | Gets or sets a scale value to apply to the X direction. This is a bindable property. |
| ScaleY | `double` | Gets or sets a scale value to apply to the Y direction. This is a bindable property. |
| Shadow | `Shadow` | Gets or sets the shadow effect cast by the element. This is a bindable property. |
| ShapeBorderColor | `Color` | Gets or sets the border color of the rating item shape. The default value of this is Grey.  This is a bindable property. |
| ShapeBorderThickness | `Thickness` | Gets or sets the border thickness of the rating item shape.  The default value is a Thickness with all values set to 1.  This is a bindable property. |
| ItemShapeSize | `double` | Gets or sets the size of the rating item shape.  The default value is 20. |
| Shape | `RatingViewShape` | Gets or sets the rating item shape.  The property is of type [`RatingViewShape`](#set-shape) and is an enumeration. The default value is Star.  This is a bindable property. |
| Spacing | `double` | Gets or sets the spacing between rating item elements.  The default value is 10.  This is a bindable property. |
| Style | `Style` | Gets or sets the unique Style for this element. |
| StyleClass | `IList<string>` | Gets or sets the style classes for the element. |
| StyleId | `string` | Gets or sets a user defined value to uniquely identify the element. |
| TranslationX | `double` | Gets or sets the X translation delta of the element. This is a bindable property. |
| TranslationY | `double` | Gets or sets the Y translation delta of the element. This is a bindable property. |
| Triggers | `IList<TriggerBase>` | Gets the list of TriggerBase objects associated to this element. This is a read-only bindable property. |
| VerticalOptions | `LayoutOptions` | Gets or sets the LayoutOptions that define how the element gets laid out in a layout cycle. This is a bindable property. |
| Visual | `IVisual` | Gets or sets a IVisual implementation that overrides the visual appearance of an element. This is a bindable property. |
| Width | `double` | Gets the current width of this element. This is a read-only bindable property. |
| WidthRequest | `double` | Gets or sets the desired width override of this element. This is a bindable property. |
| Window | `Window` | Gets the Window that is associated with an element. This is a read-only bindable property. |
| X | `double` | Gets the current X position of this element. This is a read-only bindable property. |
| Y | `double` | Gets the current Y position of this element. This is a read-only bindable property. |
| ZIndex | `int` | Gets or sets the front-to-back z-index of an element within a layout. This is a bindable property. |


## Set custom shape
The `CustomShape` property is a `string` that allows for the defining of custom rating item shape `path`. This feature empowers developers to implement unique designs, such as distinctive symbols, as rating items.

> [!IMPORTANT]
> Only when the `Shape` property is set to `Custom`, will the custom shape path be used.

The following examples sets the custom and shape properties:

```xaml
<toolkit:RatingView
	CustomShape="M 12 0C5.388 0 0 5.388 0 12s5.388 12 12 12 12-5.38 12-12c0-6.612-5.38-12-12-12z"
	Shape="Custom" />
```

The equivalent C# code is:

```csharp
RatingView ratingView = new()
{
	CustomShape = "M 12 0C5.388 0 0 5.388 0 12s5.388 12 12 12 12-5.38 12-12c0-6.612-5.38-12-12-12z",
	Shape = RatingViewShape.Custom,
};
```

For more information about custom shapes, see [Shapes.Path](/dotnet/api/microsoft.maui.controls.shapes.path).


## Set empty color
The `EmptyColor` property is a `color` that for the unfilled (empty) rating items. This allows for clear visual differentiation between rated and unrated items.

The following examples set the empty color property:

```xaml
<toolkit:RatingView
	EmptyColor="Grey" />
```

The equivalent C# code is:

```csharp
RatingView ratingView = new()
{
	EmptyColor = Colors.Grey,
};
```

## Set filled (rated) color
The `FilleColor` property is a `color` that will be applied to the filled (rated) portion of each item, offering flexibility in defining the visual aesthetic of the rating items when selected by the user.

The following examples set the filled color property:

```xaml
<toolkit:RatingView
	FilledColor="Green" />
```

The equivalent C# code is:

```csharp
RatingView ratingView = new()
{
	FilledColor = Colors.Green,
};
```

## Set is read only
The `IsReadOnly` property is a `bool` that will set the control user interface to read only.

The following examples set the is read only property:

```xaml
<toolkit:RatingView
	IsReadOnly="False" />
<toolkit:RatingView
	IsReadOnly="True" />
```

The equivalent C# code is:

```csharp
RatingView editableRatingView = new()
{
	IsReadOnly = False,
};
RatingView readOnlyRatingView = new()
{
	IsReadOnly = True,
};
```

## Set item padding
The `ItemPadding` property is a `Thickness` for the padding between the rating item and its corresponding shape, allowing for finer control over the appearance and layout of the rating items.

The following examples set the item padding property:

```xaml
<toolkit:RatingView
	ItemPadding="3, 7, 7, 3" />
```

The equivalent C# code is:

```csharp
RatingView ratingView = new()
{
	ItemPadding = new Tickness(3, 7, 7, 3),
};
```

## Set item shape size
The `ItemShapeSize` property is a `double` that customizes the shape size to fit the overall design of the application, providing the flexibility to adjust the control to various UI layouts.

The following examples set the item padding property:

```xaml
<toolkit:RatingView
	ItemShapeSize="37" />
```

The equivalent C# code is:

```csharp
RatingView ratingView = new()
{
	ItemShapeSize = 37,
};
```

## Set maximum rating
The `MaximumRating` property is a `byte` for setting the total number of items (e.g., stars, hearts, etc., or custom shapes) available for rating. This allows for ratings of any scale, such as a 5-star or 10-star system, depending on the needs of the application.

If the value is set to 1, the control will toggle the rating between 0 and 1 when clicked/tapped.  If the value is set below the current `Rating`, the rating is adjusted accordingly.

The following examples set the maximum rating property:

```xaml
<toolkit:RatingView
	MaximumRating="7" />
```

The equivalent C# code is:

```csharp
RatingView ratingView = new()
{
	MaximumRating = 7,
};
```

## Set rating fill
The `RatingFill` property is an `enum` of type `RatingFillElement` for setting how the fill is applied against the entire rating item or just the shape, enabling more nuanced visual presentation, such as filling only the interior of stars or the full item.  The available options are:

- `Shape` - (default) The filled (rated) portion of each item is applied to the item shape.
- `Item` - The filled (rated) portion of each item is applied to the item.

The following examples set the rating fill property:

```xaml
<toolkit:RatingView
	RatingFill="Shape" />
<toolkit:RatingView
	RatingFill="Item" />
```

The equivalent C# code is:

```csharp
RatingView shapeFillRatingView = new()
{
	RatingFill = RatingFillElement.Shape,
};
RatingView itemFillRatingView = new()
{
	RatingFill = RatingFillElement.Item,
};
```

## Set rating
The `Rating` property is a `double` for setting the current rating value, allowing for both pre-defined ratings (e.g., from previous user input or stored data) and updates during runtime as the user interacts with the control.

The following examples set the rating property:

```xaml
<toolkit:RatingView
	Rating="3.73" />
```

The equivalent C# code is:

```csharp
RatingView ratingView = new()
{
	Rating = 3.73,
};
```

## Handle rating changed event
The `RatingChanged` event has the argument type of `RatingChangedEventArgs`.  The event is raised when the `Rating` property is changed, and the element `IsReadOnly` is false.

The `RatingChangedEventArgs` exposes a single property:
- `Rating` - This is the new rating value.

The following examples show how to attach the  event:

```xaml
<toolkit:RatingView
	RatingChanged="RatingView_RatingChanged" />
```

The equivalent C# code is:

```csharp
	RatingView ratingView = new();
	ratingView.RatingChanged += RatingView_RatingChanged;
```

The following example is the code behind to handle the event:

```csharp
void RatingView_RatingChanged(object sender, RatingChangedEventArgs e)
{
	double newRating = e.Rating;
	// The developer can then perform further actions (such as save to DB).
}
```

## Set shape
The `Shape` property is an `enum` of type `RatingViewShape` for setting the rating item shape of the rating items, such as stars, circles, like, dislike, or any other commonly used rating icons..  The available options are:

- `Star` - (default)
- `Heart`
- `Circle`
- `Like`
- `Dislike`
- `Custom` - If set and `CustomShape` is NULL or empty, defaults to `Star`

The following examples set the rating fill property:

```xaml
<toolkit:RatingView
	Shape="Star" />
<toolkit:RatingView
	Shape="Heart" />
<toolkit:RatingView
	Shape="Circle" />
<toolkit:RatingView
	Shape="Like" />
<toolkit:RatingView
	Shape="Dislike" />
<toolkit:RatingView
	Shape="Custom" />
```

The equivalent C# code is:

```csharp
RatingView starRatingView = new()
{
	Shape = RatingViewShape.Star,
};
RatingView heartRatingView = new()
{
	Shape = RatingViewShape.Heart,
};
RatingView circleRatingView = new()
{
	Shape = RatingViewShape.Circle,
};
RatingView likeRatingView = new()
{
	Shape = RatingViewShape.Like,
};
RatingView dislikeRatingView = new()
{
	Shape = RatingViewShape.Dislike,
};
RatingView customRatingView = new()
{
	Shape = RatingViewShape.Custom,
};
```

## Set shape border color
The `ShapeBorderColor` is a `Color` for setting the border color of the rating item shape. This provides additional flexibility to create visually distinct and stylized rating shapes with custom borders.

The following examples set the shape border color property:

```xaml
<toolkit:RatingView
	ShapeBorderColor="Grey" />
```

The equivalent C# code is:

```csharp
RatingView ratingView = new()
{
	ShapeBorderColor = Colors.Grey,
};
```

## Set shape border thickness
The `ShapeBorderThickness` is a `double` for setting the thickness of the shape border. This provides additional flexibility to create visually distinct and stylized rating shapes with custom borders.

The following examples set the shape border thickness property:

```xaml
<toolkit:RatingView
	ShapeBorderThickness="3" />
```

The equivalent C# code is:

```csharp
RatingView ratingView = new()
{
	ShapeBorderThickness = 3,
};
```

## Set spacing
The `Spacing` is a `double` for setting the spacing between each rating item.

The following examples set the shape border thickness property:

```xaml
<toolkit:RatingView
	Spacing="7" />
```

The equivalent C# code is:

```csharp
RatingView ratingView = new()
{
	Spacing = 7,
};
```


## Examples

You can find examples of this control in action in the .NET MAUI Community Toolkit Sample Application:
- [XAML Syntax](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/RatingView/RatingViewXamlPage.xaml)
- [C# Syntax](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/RatingView/RatingViewCsharpPage.xaml)
- [Showcase](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/RatingView/RatingViewShowcasePage.xaml)

## API

You can find the source code for `RatingView` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/ImageSourcesViews/RatingView/RatingView.shared.cs).