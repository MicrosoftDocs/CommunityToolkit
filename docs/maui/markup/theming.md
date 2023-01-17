---
title: Theming - .NET MAUI Community Toolkit
author: bijington
description: The C# Markup package provides the ability to define property values that will swap based on the systems current theme.
ms.date: 01/13/2023
---

# Theming in C#

All platforms supported by .NET MAUI provide support for light and dark modes. It is essential to factor this into application designs to provide the best experience for the end-user. The C# Markup package provides the ability to define property values that will swap based on the systems current theme (refer to the [Microsoft documentation](/dotnet/maui/user-interface/system-theme-changes#extension-methods)).

There are two ways to define app theme values:

## 1. On a specific `BindableObject`

When building an application's user interface with C# it is possible to define the values for light and dark mode with the [`AppThemeBinding`](extensions/bindable-object-extensions.md#appthemebinding) extension method.

The following example shows how to create a `Label` with the following:

1. Set the `Text` property to display "Light Mode" when the system is in light mode and "Dark Mode" when the application is in dark mode.
1. Set the `TextColor` property to `Colors.Black` when the system is in light mode and `Colors.White` when the application is in dark mode.

```csharp
new Label()
    .AppThemeBinding(Label.TextProperty, "Light Mode", "Dark Mode")
    .AppThemeColorBinding(Label.TextColorProperty, Colors.Black, Colors.White);
```

## 2. On a `Style`

It is typically recommended to create a `Style` that can apply to multiple instances of a control and therefore simplify the code required to build an application's user interface. For this purpose there are [`AppThemeBinding`](extensions/style.md#add) methods available on the `Style<T>` class.

The following example shows how to create a `Style` for a `Label` with the same behaviour as the previous example:

1. Set the `Text` property to display "Light Mode" when the system is in light mode and "Dark Mode" when the application is in dark mode.
1. Set the `TextColor` property to `Colors.Black` when the system is in light mode and `Colors.White` when the application is in dark mode.

```csharp
var labelStyle = new Style<Label>()
    .AddAppThemeBinding(Label.TextProperty, "Light Mode", "Dark Mode")
    .AddAppThemeBinding(Label.TextColorProperty, Colors.Black, Colors.White);

new Label
{
    Style = labelStyle
};
```
