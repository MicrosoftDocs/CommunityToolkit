---
title: KeyboardExtensions - .NET MAUI Community Toolkit
author: PureWeen
description: "The KeyboardExtensions provide a series of extension methods that support interacting with the Keyboard."
ms.date: 04/12/2023
---

# KeyboardExtensions

The `KeyboardExtensions` provide a series of extension methods that support interacting with the Keyboard..

The `KeyboardExtensions` can be found under the `CommunityToolkit.Maui.Core.Extensions` namespace so just add the following line to get started:

```csharp
using CommunityToolkit.Maui.Core.Extensions;
```

## Soft Keyboard Methods

The following methods allow you to close, show, and check if the keyboard is open.

### Hide Keyboard

The `HideKeyboardAsync` method will hide the Soft Input Keyboard if it is currently visible

The following example shows how to hide the keyboard:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

entry.HideKeyboardAsync()
```

### Show Keyboard

The `ShowKeyboardAsync` method will show the Soft Input Keyboard and indicates what control you are opening it for

The following example shows how to show the keyboard for a given entry:
```csharp
using CommunityToolkit.Maui.Extensions.Core;

entry.ShowKeyboardAsync()
```

### Is SoftKeyboard Showing

The `IsSoftKeyboardShowing` method indicates if the Soft Keyboard is currently open.

The following example shows how to check if the Soft Input Keyboard is currently open and showing:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

entry.IsSoftKeyboardShowing()
```

## Examples

You can find an example of this extension in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Extensions/KeyboardExtensionsPage.xaml).

## API

You can find the source code for `KeyboardExtensions` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Extensions/KeyboardExtensions.shared.cs).