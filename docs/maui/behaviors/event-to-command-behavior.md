---
title: EventToCommandBehavior - .NET MAUI Community Toolkit
author: cliffagius
description: "The EventToCommandBehavior is a behavior that allows the user to invoke a Command through an event. It is designed to associate Commands to events exposed by controls that were not designed to support Commands. It allows you to map any arbitrary event on a control to a Command."
ms.date: 04/23/2022
---

# EventToCommandBehavior

The `EventToCommandBehavior` is a `behavior` that allows the user to invoke a `Command` through an `Event`. It is designed to associate Commands to events exposed by controls that were not designed to support Commands. It allows you to map any arbitrary event on a control to a Command.

## Syntax

The following examples show how to add an `EventToCommandBehavior` to a `Button` control and then handle the clicked event.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the EventToCommandBehavior

The `EventToCommandBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyLittleApp.MainPage">
    
    <Button>
        <Button.Behaviors>
            <toolkit:EventToCommandBehavior
                EventName="Clicked"
                Command="{Binding MyCustomCommand}" />
        </Button.Behaviors>
    </Button>
</ContentPage>
```

### C#

The `EventToCommandBehavior` can be used as follows in C#:

```csharp
class EventToCommandBehaviorPage : ContentPage
{
    public EventToCommandBehaviorPage()
    {
        var button = new Button();

        var behavior = new EventToCommandBehavior
        {
            EventName = nameof(Button.Clicked),
            Command = new MyCustomCommand()
        };

        button.Behaviors.Add(behavior);

        Content = entry;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class EventToCommandBehaviorPage : ContentPage
{
    public EventToCommandBehaviorPage()
    {
        Content = new Button()
        .Behaviors(new EventToCommandBehavior
        {
            EventName = nameof(Button.Clicked),
            Command = new MyCustomCommand()
        });                 
    }
}
```

## Accessing the EventArgs from the event

It is possible to have the `EventArgs` of the specific event passed into the `Command`. There are two ways to achieve this:

### 1. Use the generic implementation

By using the `EventToCommandBehavior<T>` implementation the `EventArgs` will be passed into the `Command` property if both the `CommandParameter` and `Converter` properties are not set. In order to refer to the [generic type](/dotnet/maui/xaml/generics) in XAML we need to make use of the `x:TypeArguments` directive.

The following example shows how to use the generic implementation to pass the `WebNavigatedEventArgs` into the command.

```xaml
<WebView Source="https://github.com">
    <WebView.Behaviors>
        <toolkit:EventToCommandBehavior
            x:TypeArguments="WebNavigatedEventArgs"
            EventName="Navigated"
            Command="{Binding WebViewNavigatedCommand}" />
    </WebView.Behaviors>
</WebView>
```


### 2. Use the Converter property

When using this `behavior` with selection or tap events exposed by `ListView` an additional converter is required. This converter converts the event arguments to a command parameter which is then passed onto the `Command`. They are also available in the .NET MAUI Community Toolkit:

* [ItemTappedEventArgsConverter](../converters/item-tapped-eventargs-converter.md)
* [SelectedItemEventArgsConverter](../converters/selected-item-eventargs-converter.md)

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| EventName | string | The name of the event that should be associated with a `Command`. |
| Command | [ICommand](xref:System.Windows.Input.ICommand) | The `Command` that should be executed. |
| CommandParameter | object | An optional parameter to forward to the `Command`. |
| EventArgsConverter | IValueConverter | An optional `IValueConverter` that can be used to convert `EventArgs` values to values passed into the `Command`. |

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/EventToCommandBehaviorPage.xaml).

## API

You can find the source code for `EventToCommandBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/EventToCommandBehavior.shared.cs).
