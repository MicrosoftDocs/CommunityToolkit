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

## Examples

You can find an example of these extension methods in action throughout the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui.Markup/blob/main/samples/CommunityToolkit.Maui.Markup.Sample/).

## API

You can find the source code for the `VisualElement` extension methods over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui.Markup/blob/main/src/CommunityToolkit.Maui.Markup/VisualElementExtensions.cs).
