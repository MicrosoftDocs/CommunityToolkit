---
title: MaxLengthReachedBehavior - .NET MAUI Community Toolkit
author: bijington
description: "The MaxLengthReachedBehavior is a behavior that allows the user to trigger an action when a user has reached the maximum length allowed on an InputView."
ms.date: 03/02/2022
---

# MaxLengthReachedBehavior

The `MaxLengthReachedBehavior` is a `Behavior` that allows the user to trigger an action when a user has reached the maximum length allowed on an `InputView`. It can either trigger a `Command` or an event depending on the user's preferred scenario. Both the `Command` and event will include the resulting text of the `InputView`.

Additionally it is possible to dismiss the keyboard when the maximum length is reached via the `ShouldDismissKeyboardAutomatically` property which defaults to `false`.

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the MaxLengthReachedBehavior

The `MaxLengthReachedBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Behaviors.MaxLengthReachedBehaviorPage">

    <Entry Placeholder="Start typing until MaxLength is reached..."
           MaxLength="100">
        <Entry.Behaviors>
            <toolkit:MaxLengthReachedBehavior 
                Command="{Binding MaxLengthReachedCommand}" />
        </Entry.Behaviors>
    </Entry>

</ContentPage>
```

### C#

The `MaxLengthReachedBehavior` can be used as follows in C#:

```csharp

class MaxLengthReachedBehaviorPage : ContentPage
{
    public MaxLengthReachedBehaviorPage()
    {
        var entry = new Entry
        {
            Placeholder = "Start typing until MaxLength is reached...",
            MaxLength = 100
        };

        var behavior = new MaxLengthReachedBehavior();
        behavior.SetBinding(
            MaxLengthReachedBehavior.CommandProperty,
            new Binding(
                nameof(ViewModel.MaxLengthReachedCommand)
            )
        );

        entry.Behaviors.Add(behavior);

        Content = entry;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class MaxLengthReachedBehaviorPage : ContentPage
{
    public MaxLengthReachedBehaviorPage()
    {
        Content = new Entry
        {
            Placeholder = "Start typing until MaxLength is reached...",
            MaxLength = 100
        }.Behaviors(
            new MaxLengthReachedBehavior().Bind(
                MaxLengthReachedBehavior.CommandProperty,
                static (ViewModel vm) => vm.MaxLengthReachedCommand));
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| `Command` | [ICommand](xref:System.Windows.Input.ICommand) | The command that is executed when the user has reached the maximum length. The parameter of the command will contain the `Text` of the `InputView`. |
| `ShouldDismissKeyboardAutomatically` | `bool` | Indicates whether or not the keyboard should be dismissed automatically when the maximum length is reached. |

## Events

|Event | Description  |
|---------|---------|
| `MaxLengthReached` | The event that is raised when the user has reached the maximum length. The event args will contain the `Text` of the `InputView`. |

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/MaxLengthReachedBehaviorPage.xaml).

## API

You can find the source code for `MaxLengthReachedBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/MaxLengthReachedBehavior.shared.cs).