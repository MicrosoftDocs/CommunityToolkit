---
title: Toast - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The Toast is a timed alert that appears at the bottom of the screen by default."
ms.date: 03/30/2022
---

# Toast

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `Toast` is a timed alert that appears at the bottom of the screen by default. It is dismissed after a configurable duration of time.

It provides simple feedback about an operation in a small alert.

## Syntax

### C#

To display `Toast` you need to create it, using the static method `Make`:

```csharp
using CommunityToolkit.Maui.Alerts;
var toast = Toast.Make(message, duration, fontSize);
await toast.Show(cancellationToken);
```

where message is your text, and duration is the enum of `ToastDuration`. The default duration is Short. `FontSize` is optional and equals 14 by default.

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| Text | `string` | Toast text message. |
| Duration | `ToastDuration` | Duration during the `Toast` is visible. |
| TextSize | `double` | `Toast` text font size. |

### ToastDuration

The `ToastDuration` enumeration defines the following members:

- `Short` - Display `Toast` for a short time.
- `Long` - Display `Toast` for a long time.

## Methods

|Method  |Description  |
|---------|---------|
| Show | Dismiss all shown toasts and display the new one. |
| Dismiss | Dismiss the current toast. |

> [!NOTE]
> You can display only 1 `Toast` at the same time. If you call the `Show` method a second time, the first `Toast` will be dismissed.

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Alerts/ToastPage.xaml.cs).

## API

You can find the source code for `Toast` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Alerts/Toast).

## Details of implementation and limitation for different platforms

1. The API allows override existing methods with your own implementation or even create your own Toast, by implementing `IToast` interface.
1. "Native" Toast is available only on Android and created by Google. Other platforms use "Container" (`UIView` for iOS and MacCatalyst, `ToastNotification` on Windows).