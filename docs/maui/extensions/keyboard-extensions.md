---
title: KeyboardExtensions - .NET MAUI Community Toolkit
author: PureWeen
description: "The KeyboardExtensions provide a series of extension methods that support interacting with the Keyboard."
ms.date: 10/23/2026
---

# KeyboardExtensions

The `KeyboardExtensions` provide a series of extension methods that support interacting with the Keyboard on controls that support text input.

The `KeyboardExtensions` can be found under the `CommunityToolkit.Maui.Core.Platform` namespace so just add the following line to get started:

```csharp
using CommunityToolkit.Maui.Core.Platform;
```

## Soft Keyboard Methods

The following methods allow you to close, show, and check if the keyboard is open.

### Hide Keyboard

The `HideKeyboardAsync` method will hide the Soft Input Keyboard if it is currently visible. It returns `true` if the platform was able to hide the keyboard.

The following example shows how to hide the keyboard for a given entry:

```csharp
using CommunityToolkit.Maui.Core.Platform;

await entry.HideKeyboardAsync(CancellationToken.None);
```

On Android, the keyboard is hidden through the window of the view that has the focus. That is the view itself while it has the focus, and otherwise the focused view of the activity's window. This makes `HideKeyboardAsync` work for an input inside a `Popup` or a modal page, which Android shows in a window of its own.

### Show Keyboard

The `ShowKeyboardAsync` method will show the Soft Input Keyboard and indicates what control you are opening it for

The following example shows how to show the keyboard for a given entry:
```csharp
using CommunityToolkit.Maui.Core.Platform;

await entry.ShowKeyboardAsync(CancellationToken.None);
```

### Is SoftKeyboard Showing

The `IsSoftKeyboardShowing` method indicates if the Soft Keyboard is currently open.

The following example shows how to check if the Soft Input Keyboard is currently open and showing:

```csharp
using CommunityToolkit.Maui.Core.Platform;

entry.IsSoftKeyboardShowing()
```

## Examples

You can find an example of this extension in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Extensions/KeyboardExtensionsPage.xaml).

## API

You can find the source code for `KeyboardExtensions` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Platform/KeyboardExtensions/KeyboardExtensions.shared.cs).
