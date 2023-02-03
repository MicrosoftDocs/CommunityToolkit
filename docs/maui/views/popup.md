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
<toolkit:Popup xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
               xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
               xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
               x:Class="MyProject.SimplePopup">

    <VerticalStackLayout>
        <Label Text="This is a very important message!" />
    </VerticalStackLayout>
    
</toolkit:Popup>
```

```csharp
public partial class SimplePopup : Popup
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

var popup = new Popup
{
    Content = new VerticalStackLayout
    {
        Children = 
        {
            new Label
            {
                Text = "This is a very important message!"
            }
        }
    }
};
```

## Presenting a Popup

Once the `Popup` has been built it can then be presented through the use of our `Popup` extension methods.

> [!IMPORTANT]
> A `Popup` can only be displayed from a `Page` or an implementation inheriting from `Page`.

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

In order to close a `Popup` a developer must call `Close` on the `Popup` itself. This is typically performed by responding to a button press from a user.

If we enhance the previous XAML example by adding an ok `Button`:

```xml
<toolkit:Popup xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
               xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
               xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
               x:Class="MyProject.SimplePopup">

    <VerticalStackLayout>
        <Label Text="This is a very important message!" />
        <Button Text="OK" 
                Clicked="OnOKButtonClicked" />
    </VerticalStackLayout>
    
</toolkit:Popup>
```

In the resulting event handler we call `Close`, this will programmatically close the `Popup`.

```csharp
void OnOKButtonClicked(object? sender, EventArgs e) => Close();
```

### Tapping outside of the Popup

By default a user can tap outside of the `Popup` to dismiss it. This can be controlled through the use of the `CanBeDismissedByTappingOutsideOfPopup` property. Setting this property to `false` will prevent a user from being able to dismiss the `Popup` by tapping outside of it.

## Returning a result

A developer will quite often seek a response from their user, the `Popup` view allows developers to return a result that can be awaited for and acted on.

We can enhance our original XAML example to show how this can be accomplished:

### XAML

By adding 2 new buttons to the XAML:

```xml
<toolkit:Popup xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
               xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
               xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
               x:Class="MyProject.SimplePopup">

    <VerticalStackLayout>
        <Label Text="This is a very important message! Do you agree?" />
        <Button Text="Yes" 
                Clicked="OnYesButtonClicked" />
        <Button Text="No"
                Clicked="OnNoButtonClicked" />
    </VerticalStackLayout>
    
</toolkit:Popup>
```

Then adding the following event handlers in the C#:

```csharp
void OnYesButtonClicked(object? sender, EventArgs e) => Close(true);

void OnNoButtonClicked(object? sender, EventArgs e) => Close(false);
```

The `Close` method allows for an `object` value to be supplied, this will be the resulting return value. In order to await the result the `ShowPopupAsync` method must be used as follows:

```csharp
using CommunityToolkit.Maui.Views;

public class MyPage : ContentPage
{
    public async Task DisplayPopup()
    {
        var popup = new SimplePopup();

        var result = await this.ShowPopupAsync(popup);

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

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| `Anchor` | `View` | Gets or sets the `View` anchor. The Anchor is where the Popup will render closest to. When an Anchor is configured the popup will appear centered over that control or as close as possible. |
| `CanBeDismissedByTappingOutsideOfPopup` | `bool` | Gets or sets a value indicating whether the popup can be dismissed by tapping outside of the Popup. On Android - when false the hardware back button is disabled. |
| `Color` | `Color` | Gets or sets the `Color` of the Popup. This color sets the native background color of the `Popup`, which is independent of any background color configured in the actual `Content`. |
| `Content` | `View` | Gets or sets the `View` content to render in the `Popup`. |
| `HorizontalOptions` | `LayoutAlignment` | Gets or sets the `LayoutAlignment` for positioning the `Popup` horizontally on the screen. |
| `Result` | `Task<object?>` | Gets the final result of the dismissed `Popup`. |
| `Size` | `Size` | Gets or sets the `Size` of the Popup Display. The Popup will always try to constrain the actual size of the `Popup` to the size of the View unless a `Size` is specified. If the `Popup` uses the `HorizontalOptions` or `VerticalOptions` properties that are not the defaults then this `Size` property is required. |
| `VerticalOptions` | `LayoutAlignment` | Gets or sets the `LayoutAlignment` for positioning the `Popup` vertically on the screen. |

## Events

|Event | Description  |
|---------|---------|
| `Closed` | The event that is dismissed event is invoked when the `Popup` is closed. |
| `Opened` | The event that is dismissed event is invoked when the `Popup` is opened. |

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/).

## API

You can find the source code for `Popup` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/tree/main/src/CommunityToolkit.Maui/Views/Popup).
