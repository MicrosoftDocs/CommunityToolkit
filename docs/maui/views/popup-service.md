---
title: PopupService - .NET MAUI Community Toolkit
author: bijington
description: The PopupService provides a mechanism for displaying Popups within an application using the MVVM pattern.
ms.date: 04/12/2022
---

# PopupService

The `PopupService` provides a mechanism for displaying [Popups](./Popup.md) within an application using the MVVM pattern.

The following sections will incrementally build on how to use the `PopupService` in a .NET MAUI application.

## Creating a Popup

In order to use the `PopupService` to present or close a `Popup` the `Popup` must first be registered. Based on the steps in [Defining your popup](./Popup.md#defining-your-popup) the following can be created.

The XAML contents of the `Popup` can be defined as:

```xaml
<ContentView
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:viewModels="clr-namespace:MyProject.ViewModels"
    x:Class="MyProject.Popups.NamePopup"
    x:DataType="viewModels:NamePopupViewModel">

    <VerticalStackLayout>
        <Label Text="What is your name?" />
        <Entry Text="{Binding Name}" />

        <Button Text="Save" Command="{Binding SaveCommand}" />
        <Button Text="Cancel" Command="{Binding CancelCommand}" />
    </VerticalStackLayout>
    
</ContentView>
```

The C# contents of the `Popup` can be defined as:

```csharp
using MyProject.ViewModels;

namespace MyProject.Popups;

public partial class NamePopup : ContentView
{
    public NamePopup(NamePopupViewModel namePopupViewModel)
    {
        InitializeComponent();
        BindingContext = namePopupViewModel;
    }
}
```

The backing view model for the `Popup` can be defined as:

```csharp
public class NamePopupViewModel : ObservableObject
{
    [ObservableProperty]
    string name = "";

    readonly IPopupService popupService;

    public NamePopupViewModel(IPopupService popupService)
    {
        this.popupService = popupService;
    }

    void OnCancel()
    {
    }

    [RelayCommand(CanExecute = nameof(CanSave))]
    void OnSave()
    {
    }

    bool CanSave() => string.IsNullOrWhitespace(Name) is false;
}
```

## Registering a Popup

In order to first use the `IPopupService` to display a popup in your application you will need to register the popup and view model with the `MauiAppBuilder`, this can be done through the use of [Register Popup View and View Model](../extensions/servicecollection-extensions.md#register-popup-view-and-view-model).

Based on the example above the following code can be added to the MauiProgram.cs file.

```csharp
builder.Services.AddTransientPopup<NamePopup, NamePopupViewModel>();
```

## Presenting a Popup

The .NET MAUI Community Toolkit provides a mechanism to instantiate and present popups in a .NET MAUI application. The popup service is automatically registered with the `MauiAppBuilder` when using the `UseMauiCommunityToolkit` initialization method. This enables you to resolve an `IPopupService` implementation in any part of your application.

The `IPopupService` makes it possible to register a popup view and its associated view model. The ability to show a `Popup` requires a developer to pass in the current `INavigation` implementation for the current window in the application. The easiest way to achieve this is through the following example.

The following example shows how to use the `IPopupService` to create and display a popup in a .NET MAUI application:

```csharp
public class MyViewModel : INotifyPropertyChanged
{
    private readonly IPopupService popupService;

    public MyViewModel(IPopupService popupService)
    {
        this.popupService = popupService;
    }

    public void DisplayPopup()
    {
        if (Application.Current?.Windows[0].Page is not Page currentPage)
        {
            throw new InvalidOperationException("Unable to retrieve current page");
        }

        this.popupService.ShowPopup<NamePopupViewModel>(currentPage.Navigation);
    }
}
```

Alternatively the caller can await the ShowPopupAsync method in order to handle a [result being returned](#returning-a-result). The `DisplayPopup` method can be rewritten as:

```csharp
public async Task DisplayPopup()
{
    if (Application.Current?.Windows[0].Page is not Page currentPage)
    {
        throw new InvalidOperationException("Unable to retrieve current page");
    }

    var name = await this.popupService.ShowPopupAsync<NamePopupViewModel>(currentPage.Navigation);
}
```

For a more concrete example please refer to our sample application and the example in [`MultiplePopupViewModel`](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/ViewModels/Views/Popup/MultiplePopupViewModel.cs)

The `IPopupService` also provides methods to handle a result being returned from a Popup as covered in [Returning a result](./popup-service.md#returning-a-result).

## Passing data to a Popup view model

When presenting a Popup we sometimes need to pass data across to the underlying view model to allow for dynamic content to be presented to the user. The `IPopupService` makes this possible through the overloads of the `ShowPopup` and `ShowPopupAsync` methods that takes a `IDictionary<string, object> shellParameters` parameter. This makes use of the `IQueryAttributable` interface provided with .NET MAUI Shell, for more information on using this please refer to [Process navigation data using a single method](/dotnet/maui/fundamentals/shell/navigation?view=net-maui-9.0#process-navigation-data-using-a-single-method).

To extend the previous example of showing a `NamePopupViewModel` and its associated Popup, we can extend the `NamePopupViewModel` to implement the `IQueryAttributable` interface as follows:

```csharp
public class NamePopupViewModel : ObservableObject, IQueryAttributable
{
    [ObservableProperty]
    public partial string Name { get; set; } = "";

    public void ApplyQueryAttributes(IDictionary<string, object> query)
    {
        Name = query["Name"] as string;
    }
}
```

Then the view model that presents the popup and passes the data can look as follows:

```csharp
public class MyViewModel : INotifyPropertyChanged
{
    private readonly IPopupService popupService;

    public MyViewModel(IPopupService popupService)
    {
        this.popupService = popupService;
    }

    public async Task DisplayPopup()
    {
        var queryAttributes = new Dictionary<string, object>
        {
            ["Name"] = "Shaun"
        };

        await this.popupService.ShowPopupAsync<NamePopupViewModel>(
            Shell.Current,
            options: null,
            queryAttributes);
    }
}
```

## Closing a Popup

The `PopupService` provides the `ClosePopup` and `ClosePopupAsync` methods that make it possible to close a `Popup` from a view model.

### Programmatically closing a Popup

Expanding on the previous example the following implementation can be added to the `OnCancel` method:

```csharp
[RelayCommand]
void OnCancel()
{
    popupService.ClosePopup();
}
```

This will result in the most recently displayed `Popup` being closed.

### Returning a result

When closing a `Popup` it is possible to return a result to the caller that presented the `Popup`.

Expanding on the previous example the following implementation can be added to the `OnSave` method:

```csharp
[RelayCommand(CanExecute = nameof(CanSave))]
void OnSave()
{
    popupService.ClosePopup(Name);
}
```

This will result in the most recently displayed `Popup` being closed and the caller being return the value in `Name`. For more information on creating a `Popup` that can return a result see [`Popup` - Returning a result](./popup/popup-result.md).

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/).

## API

You can find the source code for `Popup` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/tree/main/src/CommunityToolkit.Maui/Views/Popup).

## Additional Resources

- [`Popup` - Returning a result](./popup/popup-result.md)
- [`IPopupService`](./popup-service.md)
- [`PopupOptions` - Customizing a `Popup` behavior and appearance](./popup/popup-options.md)
