---
title: VisualElement extensions - .NET MAUI Community Toolkit
author: bijington
description: The VisualElement extensions provide a series of extension methods that support configuring the sizing, styling and behaviors of a VisualElement.
ms.date: 03/28/2022
---

# VisualElement extensions

The `VisualElement` extensions provide a series of extension methods that support configuring the sizing, styling and behaviors of a `VisualElement`.

The extensions offer the following methods:

## Height

The `Height` method sets the `HeightRequest` property on the current `VisualElement`.

The following example will create a `Label` and set it's `HeightRequest` to 50.

```csharp
new Label().Height(50);
```

## MinHeight

The `MinHeight` method sets the `MinimumHeightRequest` property on the current `VisualElement`.

The following example will create a `Label` and set it's `MinimumHeightRequest` to 50.

```csharp
new Label().MinHeight(50);
```

## Width

The `Width` method sets the `WidthRequest` property on the current `VisualElement`.

The following example will create a `Label` and set it's `WidthRequest` to 50.

```csharp
new Label().Width(50);
```

## MinWidth

The `MinWidth` method sets the `MinimumWidthRequest` property on the current `VisualElement`.

The following example will create a `Label` and set it's `MinimumWidthRequest` to 50.

```csharp
new Label().MinWidth(50);
```

## Size

The `Size` method sets the `WidthRequest` and `HeightRequest` properties on the current `VisualElement`.

The following example will create a `Label` and set it's `WidthRequest` and `HeightRequest` to 50.

```csharp
new Label().Size(50);
```

> [!NOTE]
> You can also supply the `widthRequest` and `heightRequest` separately to the `Size` method.

## MinSize

The `MinSize` method sets the `MinimumWidthRequest` and `MinimumHeightRequest` properties on the current `VisualElement`.

The following example will create a `Label` and set it's `MinimumWidthRequest` and `MinimumHeightRequest` to 50.

```csharp
new Label().MinSize(50);
```

> [!NOTE]
> You can also supply the `minimumWidthRequest` and `minimumHeightRequest` separately to the `MinSize` method.

## Style

The `Style` method sets the supplied `style` on the current `VisualElement`.

The following example will create a `Label` and set it's `Style` property.

```csharp
var labelStyle = new Style<Label>();
new Label().Style(labelStyle);
```

## Behaviors

The `Behaviors` method adds the supplied behaviors to the `Behaviors` collection on the current `VisualElement`.

The follow example will create an `Entry` and add a [`MaxLengthReachedBehavior`](../../behaviors/maximum-length-reached-behavior.md) to it.

```csharp
new Entry().Behaviors(new MaxLengthReachedBehavior());
```

## AutomationId

The `AutomationId` method sets the `AutomationId` property for the supplied `VisualElement`.

The following example will create an `Entry` and set the `AutomationId` to "PasswordEntry":

```csharp
new Entry().AutomationId("PasswordEntry");
```

## AnchorX

The `AnchorX` method sets the `AnchorX` property for the supplied `VisualElement`.

The following example will create an `Entry` and set the X component of the center point for any transform, relative to the bounds of the element to 0:

```csharp
new Entry().AnchorX(0.0);
```

## AnchorY

The `AnchorY` method sets the `AnchorY` property for the supplied `VisualElement`.

The following example will create an `Entry` and set the Y component of the center point for any transform, relative to the bounds of the element to 0.75:

```csharp
new Entry().AnchorY(0.75);
```

## Anchor

The `Anchor` method sets the `AnchorX` and `AnchorY` properties for the supplied `VisualElement`.

The following example will create a `Button` and set the X and Y components of the center point for any transform, relative to the bounds of the element to be 0.25 and 0.75:

```csharp
new Button().Anchor(0.25, 0.75);
```

## Background

The `Background` method sets the `Background` property for the supplied `VisualElement`.

The following example will create a `Button` and set the background of the element to be Blue:

```csharp
new Button().Background(new SolidColorBrush(Colors.Blue));
```

## BackgroundColor

The `BackgroundColor` method sets the `BackgroundColor` property for the supplied `VisualElement`.

The following example will create a `Button` and set the background of the element to be Red:

```csharp
new Button().BackgroundColor(Colors.Red);
```

## Clip

The `Clip` method sets the `Clip` property for the supplied `VisualElement`.

The following example will create a `Image` and apply a circular Clip:

```csharp
var ellipse = new EllipseGeometry { Center = new Point(50, 50), RadiusX = 50, RadiusY = 50 };
new Image().Clip(ellipse);
```

## FlowDirection

The `FlowDirection` method sets the `FlowDirection` property for the supplied `VisualElement`.

The following example will create an `Entry` and sets the FLowDirection to be RightToLeft:

```csharp
new Entry().FlowDirection(Microsoft.Maui.FlowDirection.RightToLeft);
```

## InputTransparent

The `InputTransparent` method sets the `InputTransparent` property for the supplied `VisualElement`.

The following example will create a `Label` that should be involved in the user interaction cycle:

```csharp
new Label().InputTransparent(false);
```

## IsEnabled

The `IsEnabled` method sets the `IsEnabled` property for the supplied `VisualElement`.

The following example will create a `Button` and set it to be disabled:

```csharp
new Button().IsEnabled(false);
```

## IsVisible

The `IsVisible` method sets the `IsVisible` property for the supplied `VisualElement`.

The following example will create a `Label` and set it to be invisible:

```csharp
new Label().IsVisible(false);
```

## Opacity

The `Opacity` method sets the `Opacity` property for the supplied `VisualElement`.

The following example will create a `Label` and set the opacity of the element to be 0.5:

```csharp
new Label().Opacity(0.5);
```

## Rotation

The `Rotation` method sets the `Rotation` property for the supplied `VisualElement`.

The following example will create a `Label` and set the rotation (in degrees) about the Z-axis (affine rotation) to a value of 45:

```csharp
new Label().Rotation(45);
```

## RotationX

The `RotationX` method sets the `RotationX` property for the supplied `VisualElement`.

The following example will create a `Label` and set the rotation (in degrees) about the X-axis (perspective rotation) to a value of 60:

```csharp
new Label().RotationX(60);
```

## RotationY

The `RotationY` method sets the `RotationY` property for the supplied `VisualElement`.

The following example will create a `Label` and set the rotation (in degrees) about the Y-axis (perspective rotation) to a value of 180:

```csharp
new Label().RotationY(180);
```

## Scale

The `Scale` method sets the `ScaleX` and `ScaleY` properties for the supplied `VisualElement`.

The following example will create a `Label` and scale the element to be one and a half times its size:

```csharp
new Label().Scale(1.5);
```

The following example will create a `Label` and scale the element to be twice as wide (X direction) and three times as high (Y direction).

```csharp
new Label().Scale(2, 3);
```

## ScaleX

The `ScaleX` method sets the `ScaleX` property for the supplied `VisualElement`.

The following example will create a `Label` and scale the element to be one and a half times (1.5x) as wide (X direction):

```csharp
new Label().ScaleX(1.5);
```

## ScaleY

The `ScaleY` method sets the `ScaleY` property for the supplied `VisualElement`.

The following example will create a `Label` and scale the element to be two times (2x) as high (Y direction):

```csharp
new Label().ScaleY(2.0);
```

## TranslationX

The `TranslationX` method sets the `TranslationX` property for the supplied `VisualElement`.

The following example will create a `Label` and set the X translation delta to 1.5:

```csharp
new Label().TranslationX(1.5);
```

## TranslationY

The `TranslationY` method sets the `TranslationY` property for the supplied `VisualElement`.

The following example will create a `Label` and set the Y translation delta to 2:

```csharp
new Label().TranslationY(2.0);
```

## ZIndex

The `ZIndex` method sets the `ZIndex` property for the supplied `VisualElement`.

The following example will create a `Label` and set the ZIndex to the value of 100:

```csharp
new Label().ZIndex(100);
```

## Examples

You can find an example of these extension methods in action throughout the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui.Markup/blob/main/samples/CommunityToolkit.Maui.Markup.Sample/).

## API

You can find the source code for the `VisualElement` extension methods over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui.Markup/blob/main/src/CommunityToolkit.Maui.Markup/VisualElementExtensions.cs).
