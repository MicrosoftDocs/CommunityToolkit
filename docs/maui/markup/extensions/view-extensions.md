---
title: View extensions - .NET MAUI Community Toolkit
author: brminnick
description: The View extensions provide a series of extension methods that support configuring the alignment of controls inheriting from View
ms.date: 05/18/2022
---

# View extensions

The `View` extensions provide a series of extension methods that support configuring the alignment of controls inheriting from `View`.

## Start

The `Start` method sets the `View.HorizontalOptions` property to `LayoutOptions.Start`.

Here's an example setting `Label.HorizontalOptions` to `LayoutOptions.Start` using `Start`:

```cs
new Label().Start()
```

## CenterHorizontal

The `CenterHorizontal` method sets the `View.HorizontalOptions` property to `LayoutOptions.Center`.

Here's an example setting `Label.HorizontalOptions` to `LayoutOptions.Center` using `CenterHorizontal`:

```cs
new Label().CenterHorizontal()
```

## End

The `End` method sets the `View.HorizontalOptions` property to `LayoutOptions.End`.

Here's an example setting `Label.HorizontalOptions` to `LayoutOptions.End` using `End`:

```cs
new Label().End()
```

## FillHorizontal

The `CenterHorizontal` method sets the `View.HorizontalOptions` property to `LayoutOptions.Fill`.

Here's an example setting `Label.HorizontalOptions` to `LayoutOptions.Fill` using `FillHorizontal`:

```cs
new Label().FillHorizontal()
```

## Top

The `Top` method sets the `View.VerticalOptions` property to `LayoutOptions.Start`.

Here's an example setting `Label.VerticalOptions` to `LayoutOptions.Start` using `Top`:

```cs
new Label().Top()
```

## CenterVertical

The `CenterVertical` method sets the `View.VerticalOptions` property to `LayoutOptions.Center`.

Here's an example setting `Label.VerticalOptions` to `LayoutOptions.Center` using `CenterVertical`:

```cs
new Label().CenterVertical()
```

## Bottom

The `Bottom` method sets the `View.VerticalOptions` property to `LayoutOptions.End`.

Here's an example setting `Label.VerticalOptions` to `LayoutOptions.End` using `Bottom`:

```cs
new Label().Bottom()
```

## FillVertical

The `FillVertical` method sets the `View.VerticalOptions` property to `LayoutOptions.Fill`.

Here's an example setting `Label.HorizontalOptions` to `LayoutOptions.Fill` using `FillVertical`:

```cs
new Label().FillVertical()
```

## Center

The `Center` method sets both the `View.HorizontalOptions` property and the `View.VerticalOptions` property to `LayoutOptions.Center`.

Here's an example setting both `Label.VerticalOptions` and `Label.HorizontalOptions` to `LayoutOptions.Center` using `Center`:

```cs
new Label().Center()
```

## Fill

The `Fill` method sets both the `View.HorizontalOptions` property and the `View.VerticalOptions` property to `LayoutOptions.Fill`.

Here's an example setting both `Label.VerticalOptions` and `Label.HorizontalOptions` to `LayoutOptions.Fill` using `Fill`:

```cs
new Label().Fill()
```

## LeftToRight

The `LeftToRight` namespace contains two extension methods, `Left` and `Right`, which align to left-to-right script.

To use the `LeftToRight` extensions, we first need to add the following `using` directive:

```cs
using CommunityToolkit.Maui.Markup.LeftToRight;
```

### Left

The `Left` method sets the `View.HorizontalOptions` property to `LayoutOptions.Start`, aligning to left-to-right script.

Here's an example setting `Label.HorizontalOptions` to `LayoutOptions.Start` using `Left`:

```cs
using CommunityToolkit.Maui.Markup.LeftToRight;

// ...

new Label().Left()
```

### Right

The `Right` method sets the `View.HorizontalOptions` property to `LayoutOptions.End`, aligning to left-to-right script.

Here's an example setting `Label.HorizontalOptions` to `LayoutOptions.End` using `Right`:

```cs
using CommunityToolkit.Maui.Markup.LeftToRight;

// ...

new Label().Right()
```

## RightToLeft

The `RightToLeft` namespace contains two extension methods, `Left` and `Right`, which align to right-to-left script.

To use the `LeftToRight` extensions, we first need to add the following `using` directive:

```cs
using CommunityToolkit.Maui.Markup.RightToLeft;
```

### Left

The `Left` method sets the `View.HorizontalOptions` property to `LayoutOptions.End`, aligning to right-to-left script.

Here's an example setting `Label.HorizontalOptions` to `LayoutOptions.End` using `Left`:

```cs
using CommunityToolkit.Maui.Markup.RightToLeft;

// ...

new Label().Left()
```

### Right

The `Right` method sets the `View.HorizontalOptions` property to `LayoutOptions.Start`, aligning to right-to-left script.

Here's an example setting `Label.HorizontalOptions` to `LayoutOptions.Start` using `Right`:

```cs
using CommunityToolkit.Maui.Markup.RightToLeft;

// ...

new Label().Right()
```
