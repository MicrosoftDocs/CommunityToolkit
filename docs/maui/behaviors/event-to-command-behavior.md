---
title: EventToCommandBehavior - .NET MAUI Community Toolkit
author: cliffagius
description: "The EventToCommandBehavior is a behavior that allows the user to invoke a Command through an event. It is designed to associate Commands to events exposed by controls that were not designed to support Commands. It allows you to map any arbitrary event on a control to a Command."
ms.date: 04/23/2022
---

# EventToCommandBehavior

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `EventToCommandBehavior` is a `behavior` that allows the user to invoke a `Command` through an `Event`. It is designed to associate Commands to events exposed by controls that were not designed to support Commands. It allows you to map any arbitrary event on a control to a Command.

When using this `behavior` with selection or tap events exposed by `ListView` an additional converter is required. This converter converts the event arguments to a command parameter which is then passed onto the Command. They are also available in the Maui Community Toolkit:

* [ItemSelectedEventArgsConverter](../converters/item-selected-eventargs-converter.md)
* [ItemTappedEventArgsConverter](../converters/item-tapped-eventargs-converter.md)

## Syntax

### XAML

The `EventToCommandBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyLittleApp.MainPage">
     
            <Button.Behaviors>
                <toolkit:EventToCommandBehavior
                    EventName="Clicked"
                    Command="{Binding MyCustomCommand}" />
            </Button.Behaviors>
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

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this behavior in C#.

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

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| EventName | string | The name of the event that should be associated with a `Command`. |
| Command | [ICommand](xref:System.Windows.Input.ICommand) | The `Command` that should be executed. |
| CommandParameter | object | An optional parameter to forward to the `Command`. |
| EventArgsConverter | [IValueConverter](xref:Xamarin.Forms.IValueConverter) | An optional `IValueConverter` that can be used to convert `EventArgs` values to values passed into the `Command`. |

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/EventToCommandBehaviorPage.xaml).

## API

You can find the source code for `EventToCommandBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/EventToCommandBehavior.shared.cs).
