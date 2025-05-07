---
title: Popup - .NET MAUI Community Toolkit
author: bijington
description: The Popup view allows developers to build their own custom UI and present it to their users.
ms.date: 04/12/2022
---

# Popup

Popups are a very common way of presenting information to a user that relates to their current task. Operating systems provide a way to show a message and require a response from the user, these alerts are typically restrictive in terms of the content a developer can provide and also the layout and appearance.

> [!NOTE]
> If you wish to present something to the user that is more subtle then checkout our [Toast](../alerts/toast.md) and [Snackbar](../alerts/snackbar.md) options.

The `Popup` view allows developers to build their own custom UI and present it to their users.

## Building a Popup

A `Popup` can be created in XAML or C#:

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Defining your Popup

Please note that if a `Popup` is created in XAML it must have a C# code behind file as well. To understand why this is required please refer to this [.NET MAUI documentation page](/dotnet/maui/xaml/runtime-load).

The easiest way to create a `Popup` is to add a new `.NET MAUI ContentView (XAML)` to your project and then change each of the files to the following:

```xaml
<ContentView
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MyProject.SimplePopup">

    <Label Text="This is a very important message!" />
    
</ContentView>
```

```csharp
public partial class SimplePopup : ContentView
{
    public SimplePopup()
    {
        InitializeComponent();
    }
}
```

> [!IMPORTANT]
> If the code behind file is not created along with the call to `InitializeComponent` then an exception will be thrown when trying to display your `Popup`.

### C#

```csharp
using CommunityToolkit.Maui.Views;

var popup = new ContentView
{
    Content = new Label
    {
        Text = "This is a very important message!"
    }
};
```

## Presenting a Popup

Once the `Popup` has been built it can then be presented through the use of our `Popup` extension methods or through the [`IPopupService`](popup-service.md) implementation from this toolkit.

> [!IMPORTANT]
> A `Popup` can only be displayed from a `Page` or an `INavigation` implementation.

```csharp
using CommunityToolkit.Maui.Views;

public class MyPage : ContentPage
{
    public void DisplayPopup()
    {
        var popup = new SimplePopup();

        this.ShowPopup(popup);
    }
}
```

## Closing a Popup

There are 2 different ways that a `Popup` can be closed; programmatically or by tapping outside of the popup.

### Programmatically closing a Popup

In order to close a `Popup` a developer must call `Close` or `CloseAsync` on the `Popup` itself. This is typically performed by responding to a button press from a user.

We can enhance the previous XAML example by adding an **OK** `Button`:

```xaml
<VerticalStackLayout
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MyProject.SimplePopup">

    <Label Text="This is a very important message!" />
    <Button Text="OK" 
            Clicked="OnOKButtonClicked" />
    
</VerticalStackLayout>
```

In the resulting event handler we call `Close`, this will programmatically close the `Popup`.

> [!NOTE]
> `Close()` is a fire-and-forget method. It will complete and return to the calling thread before the operating system has dismissed the `Popup` from the screen. If you need to pause the execution of your code until the operating system has dismissed the `Popup` from the screen, use instead `CloseAsync()`.

```csharp
public partial class MySimplePopup : VerticalStackLayout
{
    // ...

    void OnOKButtonClicked(object? sender, EventArgs e) => Close();
}
```

In the resulting event handler we call `CloseAsync`, this will programmatically close the `Popup` allowing the caller to `await` the method until the operating system has dismissed the `Popup` from the screen.

```csharp
public partial class MySimplePopup : VerticalStackLayout
{
    // ...

    async void OnOKButtonClicked(object? sender, EventArgs e) 
    {
        var cts = new CancellationTokenSource(TimeSpan.FromSeconds(5));

         await CloseAsync(token: cts.Token);
         await Toast.Make("Popup Dismissed By Button").Show();
    }
}
```

### Tapping outside of the Popup

By default a user can tap outside of the `Popup` to dismiss it. This can be controlled through the use of the `PopupOptions.CanBeDismissedByTappingOutsideOfPopup` property. Setting this property to `false` will prevent a user from being able to dismiss the `Popup` by tapping outside of it. See [PopupOptions](#popupoptions) for more details.

## Returning a result

A developer will quite often seek a response from their user, the `Popup` view allows developers to return a result that can be awaited for and acted on.

We can enhance our original XAML example to show how this can be accomplished:

### XAML

By adding 2 new buttons to the XAML:

```xaml
<VerticalStackLayout 
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MyProject.SimplePopup">

    <Label Text="This is a very important message! Do you agree?" />
    <Button Text="Yes" 
            Clicked="OnYesButtonClicked" />
    <Button Text="No"
            Clicked="OnNoButtonClicked" />
    
</VerticalStackLayout>
```

Then adding the following event handlers in the C#:

```csharp
async void OnYesButtonClicked(object? sender, EventArgs e)
{
    var cts = new CancellationTokenSource(TimeSpan.FromSeconds(5));
    await CloseAsync(true, cts.Token);
}

async void OnNoButtonClicked(object? sender, EventArgs e)
{
    var cts = new CancellationTokenSource(TimeSpan.FromSeconds(5));
    await CloseAsync(false, cts.Token);
}
```

The `Close` method allows for an `object` value to be supplied, this will be the resulting return value. In order to await the result the `ShowPopupAsync` method must be used as follows:

```csharp
using CommunityToolkit.Maui.Views;

public class MyPage : ContentPage
{
    public async Task DisplayPopup()
    {
        var popup = new SimplePopup();

        var result = await this.ShowPopupAsync(popup, CancellationToken.None);

        if (result is bool boolResult)
        {
            if (boolResult)
            {
                // Yes was tapped
            }
            else
            {
                // No was tapped
            }
        }
    }
}
```

> [!NOTE]
> In order to handle the tapping outside of a `Popup` when also awaiting the result you can change the value that is returned through the `ResultWhenUserTapsOutsideOfPopup` property.

## PopupOptions

It is possible to further customize the appearance of the `Popup` through the use of the `PopupOptions` class.

The `PopupOptions` class provides the following bindable properties to make it possible for developers to dynamic control the property values.

|Property  |Type  |Description  |
|---------|---------|---------|
| `CanBeDismissedByTappingOutsideOfPopup` | `bool` | Gets or sets a value indicating whether the popup can be dismissed by tapping outside of the Popup. On Android - when false the hardware back button is disabled. |
| `OnTappingOutsideOfPopup` | `Action` | Gets or sets the `Action` to be executed when the user taps outside the `Popup`. |
| `PageOverlayColor` | `Color` | Gets or sets the `Color` of the overlay behind the `Popup`. |
| `Shape` | `Shape` | Gets or sets the border shape for the `Popup`. Set this to `null` to remove any border styling. |
| `Shadow` | `Shadow` | Gets or sets the `Shadow` of the `Popup`. Set this to `null` to remove any shadow. |

## Events

The `Popup` class provides the following events that can be subscribed to.

|Event | Description  |
|---------|---------|
| `Closed` | Occurs when the `Popup` is closed. |
| `Opened` | Occurs when the `Popup` is opened. |

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/).

## API

You can find the source code for `Popup` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/tree/main/src/CommunityToolkit.Maui/Views/Popup).
