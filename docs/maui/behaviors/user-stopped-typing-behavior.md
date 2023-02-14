---
title: UserStoppedTypingBehavior - .NET MAUI Community Toolkit
author: cliffagius
description: "The UserStoppedTypingBehavior is a Behavior that will trigger an action when a user has stopped data input on controls for example Entry, SearchBar and Editor. Examples of its usage include triggering a search when a user has stopped entering their search query."
ms.date: 04/13/2022
---

# UserStoppedTypingBehavior

The `UserStoppedTypingBehavior` is a `Behavior` that will trigger an action when a user has stopped data input on controls for example `Entry`, `SearchBar` and `Editor`. Examples of its usage include triggering a search when a user has stopped entering their search query.

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the UserStoppedTypingBehavior

The `UserStoppedTypingBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyLittleApp.MainPage">
     
           <Entry Placeholder="Start typing when you stop the behavior will trigger...">
                <Entry.Behaviors>
                    <toolkit:UserStoppedTypingBehavior 
                        Command="{Binding SearchCommand}"
                        StoppedTypingTimeThreshold="1000"
                        MinimumLengthThreshold="3"
                        ShouldDismissKeyboardAutomatically="True" />
                </Entry.Behaviors>
            </Entry>
</ContentPage>
```

### C#

The `UserStoppedTypingBehavior` can be used as follows in C#:

```csharp
class UserStoppedTypingBehaviorPage : ContentPage
{
    public UserStoppedTypingBehaviorPage()
    {
        var behavior = new UserStoppedTypingBehavior()
        {
            StoppedTypingTimeThreshold = 1000,
            MinimumLengthThreshold = 3,
            ShouldDismissKeyboardAutomatically = true
        };

        behavior.SetBinding(UserStoppedTypingBehavior.CommandProperty, 
        nameof(ViewModel. SearchCommand);

        var entry = new Entry
        {
            Placeholder = "Start typing when you stop the behavior will trigger..."
        };

        entry.Behaviors.Add(behavior);
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class UserStoppedTypingBehaviorPage : ContentPage
{
    public UserStoppedTypingBehaviorPage()
    {
        Content = new Entry
        {
            Placeholder = "Start typing when you stop the behavior will trigger..."
        }
        .Behaviors(new UserStoppedTypingBehavior
        {
            StoppedTypingTimeThreshold = 1000,
            MinimumLengthThreshold = 3,
            ShouldDismissKeyboardAutomatically = true
        }
        .Bind(
            UserStoppedTypingBehavior.CommandProperty, 
            static (ViewModel vm) => vm.SearchCommand,
            mode: BindingMode.OneTime));
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| Command | [ICommand](xref:System.Windows.Input.ICommand) | The command to execute when the user has stopped providing input. |
| MinimumLengthThreshold | int | The minimum length of the input value required before the command will be executed. |
| ShouldDismissKeyboardAutomatically | bool | Indicates whether or not the keyboard should be dismissed automatically. |
| StoppedTypingTimeThreshold | int | The time of inactivity in milliseconds after which the command will be executed. |

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/UserStoppedTypingBehaviorPage.xaml).

## API

You can find the source code for `UserStoppedTypingBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/UserStoppedTypingBehavior.shared.cs).
