---
title: TextAlignment extensions - .NET MAUI Community Toolkit
author: brminnick
description: The TextAlignment extensions provide a series of extension methods that support configuring the text alignment of controls implementing ITextAlignment.
ms.date: 05/18/2022
---

# TextAlignment extensions

The `TextAlignment` extensions provide a series of extension methods that support configuring the text alignment of controls implementing `ITextAlignment`.

## TextStart

The `TextStart` method sets the `ITextAlignment.HorizontalTextAlignment` property to `TextAlignment.Start`.

Here's an example setting `Label.HorizontalTextAlignment` to `TextAlignment.Start` using `TextStart`:

```cs
new Label().TextStart()
```

## TextCenterHorizontal

The `TextCenterHorizontal` method sets the `ITextAlignment.HorizontalTextAlignment` property to `TextAlignment.Center`.

Here's an example setting `Label.HorizontalTextAlignment` to `TextAlignment.Center` using `TextCenterHorizontal`:

```cs
new Label().TextCenterHorizontal()
```

## TextEnd

The `TextEnd` method sets the `ITextAlignment.HorizontalTextAlignment` property to `TextAlignment.End`.

Here's an example setting `Label.HorizontalTextAlignment` to `TextAlignment.End` using `TextEnd`:

```cs
new Label().TextEnd()
```

## TextTop

The `TextTop` method sets the `ITextAlignment.VerticalTextAlignment` property to `TextAlignment.Start`.

Here's an example setting `Label.VerticalTextAlignment` to `TextAlignment.Start` using `TextTop`:

```cs
new Label().TextTop()
```

## TextCenterVertical

The `TextCenterVertical` method sets the `ITextAlignment.VerticalTextAlignment` property to `TextAlignment.Center`.

Here's an example setting `Label.VerticalTextAlignment` to `TextAlignment.Center` using `TextCenterVertical`:

```cs
new Label().TextCenterVertical()
```

## TextBottom

The `TextBottom` method sets the `ITextAlignment.VerticalTextAlignment` property to `TextAlignment.End`.

Here's an example setting `Label.VerticalTextAlignment` to `TextAlignment.End` using `TextBottom`:

```cs
new Label().TextBottom()
```

## TextCenter

The `TextCenter` method sets both the `ITextAlignment.HorizontalTextAlignment` property and the `ITextAlignment.VerticalTextAlignment` property to `TextAlignment.Center`.

Here's an example setting both `Label.VerticalTextAlignment` and `Label.HorizontalTextAlignment` to `TextAlignment.Center` using `TextCenter`:

```cs
new Label().TextCenter()
```

## LeftToRight

The `LeftToRight` namespace contains two extension methods, `TextLeft` and `TextRight`, which align to left-to-right script.

To use the `LeftToRight` extensions, we first need to add the following `using` directive:

```cs
using CommunityToolkit.Maui.Markup.LeftToRight;
```

### TextLeft

The `TextLeft` method sets the `ITextAlignment.HorizontalTextAlignment` property to `TextAlignment.Start`, aligning to left-to-right script.

Here's an example setting `Label.HorizontalTextAlignment` to `TextAlignment.Start` using `TextLeft`:

```cs
using CommunityToolkit.Maui.Markup.LeftToRight;

// ...

new Label().TextLeft()
```

### TextRight

The `TextRight` method sets the `ITextAlignment.HorizontalTextAlignment` property to `TextAlignment.End`, aligning to left-to-right script.

Here's an example setting `Label.HorizontalTextAlignment` to `TextAlignment.End` using `TextRight`:

```cs
using CommunityToolkit.Maui.Markup.LeftToRight;

// ...

new Label().TextRight()
```

## RightToLeft

The `RightToLeft` namespace contains two extension methods, `TextLeft` and `TextRight`, which align to right-to-left script.

To use the `LeftToRight` extensions, we first need to add the following `using` directive:

```cs
using CommunityToolkit.Maui.Markup.RightToLeft;
```

### TextLeft

The `TextLeft` method sets the `ITextAlignment.HorizontalTextAlignment` property to `TextAlignment.End`, aligning to right-to-left script.

Here's an example setting `Label.HorizontalTextAlignment` to `TextAlignment.End` using `TextLeft`:

```cs
using CommunityToolkit.Maui.Markup.RightToLeft;

// ...

new Label().TextLeft()
```

### TextRight

The `TextRight` method sets the `ITextAlignment.HorizontalTextAlignment` property to `TextAlignment.Start`, aligning to right-to-left script.

Here's an example setting `Label.HorizontalTextAlignment` to `TextAlignment.Start` using `TextRight`:

```cs
using CommunityToolkit.Maui.Markup.RightToLeft;

// ...

new Label().TextRight()
```
