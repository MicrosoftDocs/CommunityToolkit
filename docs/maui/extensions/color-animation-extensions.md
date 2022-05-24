---
title: ColorAnimationExtensions - .NET MAUI Community Toolkit
author: bijington
description: "The ColorAnimationExtensions provide a series of extension methods that support animating the Color related properties of a VisualElement."
ms.date: 04/22/2022
---

# ColorAnimationExtensions

The `ColorAnimationExtensions` provide a series of extension methods that support animating the `Color` related properties of a `VisualElement`.

The `ColorAnimationExtensions` can be found under the `CommunityToolkit.Maui.Extensions` namespace so just add the following line to get started:

```csharp
using CommunityToolkit.Maui.Extensions;
```

## BackgroundColorTo

The `BackgroundColorTo` method allows you to animate the `BackgroundColor` change of a `VisualElement`.

### Syntax

The following example shows how to animate the `BackgroundColor` from `Colors.White` to `Colors.Red` for a `Label`:

```csharp
using CommunityToolkit.Maui.Extensions;

var label = new Label
{
    BackgroundColor = Colors.White
};

await label.BackgroundColorTo(Colors.Red);
```

The full argument list for the `BackgroundColorTo` method is:

- `color`, of type `Color`, is the target color to animate the `VisualElement`'s `BackgroundColor` to.
- `rate`, of type `uint`, is the time, in milliseconds, between the frames of the animation. This is an optional argument, whose default value is 16.
- `length`, of type `uint`, is the duration, in milliseconds, of the animation. This is an optional argument, whose default value is 250.
- `easing`, of type `Easing`, is the easing function to be used in the animation. This is an optional argument, whose default value is `null`.

## TextColorTo

The `TextColorTo` method allows you to animate the `TextColor` change of an `ITextStyle` implementation.

```csharp
using CommunityToolkit.Maui.Extensions;

var label = new Label
{
    TextColor = Colors.Green
};

await label.TextColorTo(Colors.Red);
```

The full argument list for the `TextColorTo` method is:

- `color`, of type `Color`, is the target color to animate the `VisualElement`'s `BackgroundColor` to.
- `rate`, of type `uint`, is the time, in milliseconds, between the frames of the animation. This is an optional argument, whose default value is 16.
- `length`, of type `uint`, is the duration, in milliseconds, of the animation. This is an optional argument, whose default value is 250.
- `easing`, of type `Easing`, is the easing function to be used in the animation. This is an optional argument, whose default value is `null`.

> [!NOTE]
> The `TextColorTo` method is generated at compilation time through the use of Source Generators. This is due to the fact that `ITextStyle.TextColor` is readonly.
> You can find the source code for the Source Generator on our [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.SourceGenerators/Generators/TextColorToGenerator.cs)

## Examples

You can find an example of this extension in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Extensions/ColorAnimationExtensionsPage.xaml).

## API

You can find the source code for `ColorAnimationExtensions` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Extensions/ColorAnimationExtensions.shared.cs).