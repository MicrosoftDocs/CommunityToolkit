---
title: Popup - .NET MAUI Community Toolkit
author: bijington
description: The Popup view allows developers to build their own custom UI and present it to their users.
ms.date: 04/12/2022
---

# Popup

Popups are a common way of presenting information to a user that relates to their current task. Operating systems provide a way to show a message and require a response from the user, these alerts are typically restrictive in terms of the content a developer can provide and also the layout and appearance.

> [!NOTE]
> If you wish to present something to the user that is more subtle then checkout our [Toast](../alerts/toast.md) and [Snackbar](../alerts/snackbar.md) options.

The `Popup` view allows developers to build their own custom UI and present it to their users.

The .NET MAUI Community Toolkit provides 2 approaches to create a `Popup` that can be shown in a .NET MAUI application. These approaches will depend on the use case. This page focuses on the simplest form of `Popup` - simply rendering an overlay in an application. For a more advanced approach, enabling the ability to return a result from the `Popup`, please refer to [Popup - Returning a result](./popup/popup-result.md).

## Displaying a Popup

The .NET MAUI Community Toolkit provides multiple approaches to display a `Popup` in a .NET MAUI application:

1. In a `ContentPage`, call to the `this.ShowPopupAsync()` extension method, passing in a `View` to display in the Popup
    - **Note:** To further customize a Popup, please refer to the [**PopupOptions** documentation](./popup/popup-options.md).
2. Returning a result from the `Popup`
    - Please refer to the [**Popup - Returning a result** documentation](./popup/popup-result.md).
3. Using the `PopupService`
    - Please refer to the [**PopupService** documentation](./popup-service.md).

The documentation below demonstrates the simplest way to display a Popup using the `.ShowPopupAsync()` extension method. This method returns a `Task<IPopupResult>` that will complete when the Popup closes. The `PopupOptions` provided are optional.

```cs
public class MainPage : ContentPage
{
    // ...

    async void DisplayPopupButtonClicked(object? sender, EventArgs e)
    {
        await this.ShowPopupAsync(new Label
        {
            Text = "This is a very important message!"
        }, new PopupOptions
        {
            CanBeDismissedByTappingOutsideOfPopup = false,
            Shape = new RoundRectangle
            {
                CornerRadius = new CornerRadius(20, 20, 20, 20),
                StrokeThickness = 2,
                Stroke = Colors.LightGray
            }
        })

        /**** Alternatively, Shell.Current can be used to display a Popup

        await Shell.Current.ShowPopupAsync(new Label
        {
            Text = "This is a very important message!"
        }, new PopupOptions
        {
            CanBeDismissedByTappingOutsideOfPopup = false,
            Shape = new RoundRectangle
            {
                CornerRadius = new CornerRadius(20, 20, 20, 20),
                StrokeThickness = 2,
                Stroke = Colors.LightGray
            }
        })
        ****/
    }
}
```

![Popup with padding](../images/views/popup/popup-with-padding.png "Popup rendering with padding around a simple label")

Alternatively, a `Popup` can be created in XAML or C# and passed into `ShowPopupAsync()`.

### Building a Popup in XAML

The easiest way to create a `Popup` is to add a new `.NET MAUI ContentView (XAML)` to your project. This will create 2 files: a _*.xaml_ file and a _*.xaml.cs_ file. 

Replace the contents of _*.xaml_ with the following:

```xaml
<ContentView
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MyProject.SimplePopup"
    Padding="10">

    <Label Text="This is a very important message!" />
    
</ContentView>
```

The default values for `HorizontalOptions` and `VerticalOptions` will result in the `Popup` being displayed in the center of page that it overlays.

A popup will present with a default `Padding` of 15. In order to make the `SimplePopup` look better a `Padding` of 10 has been added.

### Presenting a Popup Created in XAML

Once the `Popup` has been created in XAML, it can then be presented through the use of the `Popup` extension methods used on a `Page`, `Shell` or an `INavigation`, or through the [`IPopupService`](popup-service.md) implementation from this toolkit.

The following example shows how to instantiate and show the `SimplePopup` created in the previous example through an extension method on a `ContentPage`.

```csharp
using CommunityToolkit.Maui.Views;

public class MyPage : ContentPage
{
    public async Task DisplayPopup(CancellationToken token)
    {
        var popup = new SimplePopup();

        await this.ShowPopupAsync(popup, PopupOptions.Empty, token);
    }
}
```

![Popup with padding](../images/views/popup/popup-with-padding.png "Popup rendering with padding around a simple label")

## Closing a Popup

There are 2 different ways that a `Popup` can be closed: 

1. A Popup can be closed programmatically 
2. A Popup can be closed when a user taps outside of the popup
    - **Note** To prevent a Popup from closing when a user taps outside of it, set `PopupOptions.CanBeDismissedByTappingOutsideOfPopup` to `false`

### 1. Programmatically closing a Popup

There are 3 options to close a `Popup` programatically:

1. In a `ContentPage`, use the `this.ClosePopupAsync()` extension method
2. In an app using `Shell`, use `Shell.Current.ClosePopupAsync()` extension method
3. Use the `PopupService`
    - Please refer to the [**PopupService** documentation](./popup-service.md).

In the example below, we demonstrate how to use `this.ClosePopupAsync()` in a `ContentPage`. To learn how to use `PopupService` to close a Popup, please refer to the [**PopupService** documentation](./popup-service.md). 

```csharp
using CommunityToolkit.Maui.Views;

public class MyPage : ContentPage
{
    public async Task DisplayAutomaticallyClosingPopup(Timespan displayTimeSpan, CancellationToken token)
    {
        var popup = new SimplePopup();

        // This Popup is closed programmatically after 2 seconds
        this.ShowPopup(popup, new PopupOptions
        {
            CanBeDismissedByTappingOutsideOfPopup = false
        });

        await Task.Delay(TimeSpan.FromSeconds(displayTimeSpan), token);

        await this.ClosePopupAsync(token);

        /**** Alternatively, Shell.Current can be used to close a Popup
        Shell.Current.ShowPopup(popup, new PopupOptions
        {
            CanBeDismissedByTappingOutsideOfPopup = false
        });

        await Task.Delay(TimeSpan.FromSeconds(displayTimeSpan), token);

        await Shell.Current.ClosePopupAsync(token);
        ***/

    }
}
```

### 2. Tapping outside of the Popup

By default a user can tap outside of the `Popup` to dismiss it. This can be controlled through the use of the `PopupOptions.CanBeDismissedByTappingOutsideOfPopup` property. Setting this property to `false` will prevent a user from being able to dismiss the `Popup` by tapping outside of it. See [PopupOptions](./popup/popup-options.md) for more details.

## PopupOptions

The `PageOverlayColor`, `Shape`, `Shadow` can all be customized for Popup. See [PopupOptions](./popup/popup-options.md) for more details.

## Events

The `Popup` class provides the following events that can be subscribed to.

|Event | Description  |
|---------|---------|
| `Closed` | Occurs when the `Popup` is closed. |
| `Opened` | Occurs when the `Popup` is opened. |

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/Popup/).

## API

You can find the source code for `Popup` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/tree/main/src/CommunityToolkit.Maui/Views/Popup).

## Additional Resources

- [`IPopupService`](popup-service.md)
- [`Popup` - Returning a result](./popup/popup-result.md)
- [`PopupOptions` - Customizing a `Popup` behavior and appearance](./popup/popup-options.md)