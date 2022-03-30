---
title: Snackbar - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The Snackbar is a timed alert that appears at the bottom of the screen by default."
ms.date: 03/30/2022
---

# Snackbar

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `Snackbar` is a timed alert that appears at the bottom of the screen by default. It is dismissed after a configurable duration of time. `Snackbar` is fully customizable and can be anchored to any `IView`.

The `Snackbar` informs users of a process that an app has performed or will perform. It appears temporarily, towards the bottom of the screen.

## Syntax

### C#

To display `Snackbar` you need to create it, using the static method `Make`:

```csharp
using CommunityToolkit.Maui.Alerts;
var options = new SnackbarOptions
{
    BackgroundColor = Colors.Red,
    TextColor = Colors.Green,
    ActionButtonTextColor = Colors.Yellow,
    CornerRadius = new CornerRadius(10),
    Font = Font.SystemFontOfSize(14),
    ActionButtonFont = Font.SystemFontOfSize(14),
    CharacterSpacing = 0.5
};
var snackbar = Snackbar.Make(text, action, actionButtonText, duration, visualOptions, anchorVisualElement);
await snackbar.Show(token);
```

`Text` is required for the `Snackbar`. All other parameters are optional.

There is also an extension method, which allows anchor the `Snackbar` to any `VisualElement`:

```csharp
await MyVisualElement.DisplaySnackbar(
    "Snackbar is awesome. It is anchored to my visual element",
    RunAwesomeAction,
    "Make snackbar even better",
    TimeSpan.FromSeconds(5),
    options,
    CancellationToken.None);
```	

It is also possible to subscribe to the `SnackBar` events: `Shown` and `Dismissed` and check if SnackBar is shown with static `IsShown` property.

```csharp
Snackbar.Shown += (s, e) => { Console.WriteLine(Snackbar.IsShown); };
Snackbar.Dismissed += (s, e) => { Console.WriteLine(Snackbar.IsShown); };
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| Text | `string` | Text message. **Required** |
| Action | `Action` | Action to invoke on action button click. |
| ActionButtonText | `string` | Action button text. |
| Anchor | `IView` | `Snackbar` anchor. `Snackbar` appears near this view. Can be `null`. |
| Duration | `TimeSpan` | `Snackbar` duration. |
| VisualOptions | `SnackbarOptions` | `Snackbar` visual options. |

### SnackbarOptions

The `SnackbarOptions` allows customize the default `Snackbar` style.

#### Properties

|Property  |Type  |Description  |Default value
|---------|---------|---------|---------|
| CharacterSpacing | `double` | Message character spacing. | 0.0d |
| Font | `Font` | Message font. | Default system font of size 14 |
| TextColor | `Color` | Message text color. | Black |
| ActionButtonFont | `Font` | Action button font. | Default system font of size 14 |
| ActionButtonTextColor | `Color` | Action button text color. | Black |
| BackgroundColor | `Color` | Background color. | LightGray |
| CornerRadius | `CornerRadius` | Corner radius. | (4, 4, 4, 4) |

## Methods

|Method  |Description  |
|---------|---------|
| Show | Dismiss all shown snackbars and display the new one. |
| Dismiss | Dismiss the current snackbar. |

> [!NOTE]
> You can display only 1 `Snackbar` at the same time. If you call the `Show` method a second time, the first `Snackbar` will be dismissed.

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Alerts/SnackbarPage.xaml.cs).

## API

You can find the source code for `Snackbar` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Alerts/Snackbar).

## Details of implementation and limitation for different platforms

1. The API allows override existing methods with your own implementation or even create your own Snackbar, by implementing `ISnackbar` interface.
1. "Native" Snackbar is available only on Android and created by Google. Other platforms use "Container" (`UIView` for iOS and MacCatalyst, `ToastNotification` on Windows).
1. `Snackbar` on Windows can't be anchored to `VisualElement` and is always displayed as a default Windows Notification.