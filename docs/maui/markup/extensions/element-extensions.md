---
title: Element extensions - .NET MAUI Community Toolkit
author: brminnick
description: The Element extensions provide a series of extension methods that support configuring the sizing, styling and behaviors of an Element.
ms.date: 03/28/2022
---

# Element extensions

The `Element` extensions provide a series of extension methods that support configuring the padding, effects, font attributes, dynamic resources, text, and text color of an `Element`.

## Padding

The `Padding` method sets the `Padding` property on an `IPaddingElement`.

The following example sets the `Padding` to `new Thickness(5, 10)`:

```csharp
new Button().Padding(5, 10);
```

The following examples set the `Padding` to `new Thickness(10, 20, 30, 40)`:

```csharp
new Button().Padding(new Thickness(10, 20, 30, 40));
```

```csharp
new Button().Paddings(10, 20, 30, 40);
```

## RemoveDynamicResources

The `RemoveDynamicResources` method removes all dynamic resources from a specified `BindableObject`.

The following example removes the `DynamicResource` from the `BackgroundColorProperty` and `TextColorProperty`:

```csharp
var button = new Button().DynamicResources(
    (Button.BackgroundColorProperty, "ButtonBackgroundColor"),
    (Button.TextColorProperty, "ButtonTextColor"));

button.RemoveDynamicResources(Button.BackgroundColorProperty, Button.TextColorProperty);
```

## Effects

The `Effects` method attaches the provided `Effect` to an `Element`.

The following example attaches the `ShadowEffect` and `TouchEffect` to the `Element`:

```csharp
new Button().Effects(new ShadowEffect(), new TouchEffect());
```

## Font Size

The `FontSize` method sets the `FontSize` property on an `IFontElement` element.

The following example sets the `FontSize` to `12`:

```csharp
new Button().FontSize(12);
```

## Bold

The `Bold` method sets `FontAttributes = FontAttributes.Bold` on an `IFontElement` element.

The following example sets the button font to bold:

```csharp
new Button().Bold()
```

## Italic

The `Italic` method sets `FontAttributes = FontAttributes.Italic` on an `IFontElement` element.

The following example sets the button font to italic:

```csharp
new Button().Italic()
```

## Font

The `Font` method sets `FontFamily`, `FontSize`, and `FontAttributes` on an `IFontElement` element.

The following example sets the button font to italic:

```csharp
new Button().Font(family: "OpenSansRegular", size: 12.5, bold: true, italic: true);
```

## TextColor

The `TextColor` method sets the `TextColor` property on an `ITextStyle` element.

The following example sets the `TextColor` to `Colors.Green`:

```csharp
new Button().TextColor(Colors.Green);
```

## Text

The `Text` methods sets the `Text` property on an `IText` element.

The following example sets the `Text` to `"Tap Here"`:

```csharp
new Button().Text("Tap Here");
```

The following example sets the `Text` to `"Tap Here"` and sets the `TextColor` property to `Colors.Blue`:

```csharp
new Button().Text("Tap Here", Colors.Blue);
```
