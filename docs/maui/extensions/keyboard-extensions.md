---
title: KeyboardExtensions - .NET MAUI Community Toolkit
author: PureWeen
description: "The KeyboardExtensions provide a series of extension methods that support interacting with the Keyboard."
ms.date: 11/20/2026
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

On Android 11 to 12L (API 30 to 32), the keyboard can close again right after `ShowKeyboardAsync` when an earlier hide is still animating. So when you call `ShowKeyboardAsync` within 2 seconds of a hide by the toolkit (`HideKeyboardAsync`, or a behavior that dismisses the keyboard), the toolkit checks the keyboard every 0.4 seconds for up to 2 seconds and shows it again if it has closed. It stops once the keyboard is open at two checks in a row (0.8 seconds at the earliest). Until then, it also undoes the user pressing Back. Calling `HideKeyboardAsync` or moving the focus away stops it.

### Is SoftKeyboard Showing

The `IsSoftKeyboardShowing` method indicates if the Soft Keyboard is currently open.

The following example shows how to check if the Soft Input Keyboard is currently open and showing:

```csharp
using CommunityToolkit.Maui.Core.Platform;

bool isSoftKeyboardShowing = entry.IsSoftKeyboardShowing();
```

On iOS and Windows, the state of the keyboard is read on the UI thread. When you call `IsSoftKeyboardShowing` from another thread, it blocks until the UI thread has answered. On the same platforms, `HideKeyboardAsync` and `ShowKeyboardAsync` do their work on the UI thread, and their tasks complete once the UI thread has done it.

## Examples

You can find an example of this extension in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Extensions/KeyboardExtensionsPage.xaml).

## API

You can find the source code for `KeyboardExtensions` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Platform/KeyboardExtensions/KeyboardExtensions.shared.cs).
