---
title: MaskedBehavior - .NET MAUI Community Toolkit
author: bijington
description: "The MaskedBehavior is a Behavior that allows the user to define an input mask for data entry."
ms.date: 04/16/2022
---

# MaskedBehavior

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `MaskedBehavior` is a `Behavior` that allows the user to define an input mask for data entry. Adding this behavior to an `InputView` (e.g. an `Entry`) control will force the user to only input values matching a given mask. Examples of its usage include input of a credit card number or a phone number.

## Syntax

The following examples show how to add the `MaskedBehavior` to an `Entry` to aid a user when entering a 16 digit credit card number.

### XAML

The `MaskedBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.MaskedBehaviorPage">

    <Entry Keyboard="Numeric">
        <Entry.Behaviors>
            <toolkit:MaskedBehavior Mask="XXXX XXXX XXXX XXXX" />
        </Entry.Behaviors>
    </Entry>

</ContentPage>
```

### C#

The `MaskedBehavior` can be used as follows in C#:

```csharp

class MaskedBehaviorPage : ContentPage
{
    public MaskedBehaviorPage()
    {
        var entry = new Entry
        {
            Keyboard = Keyboard.Numeric
        };

        var behavior = new MaskedBehavior
        {
            Mask = "XXXX XXXX XXXX XXXX"
        };

        entry.Behaviors.Add(behavior);

        Content = entry;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class MaskedBehaviorPage : ContentPage
{
    public MaskedBehaviorPage()
    {
        Content = new Entry
        {
            Keyboard = Keyboard.Numeric
        }.Behaviors(new MaskedBehavior
        {
            Mask = "XXXX XXXX XXXX XXXX"
        });
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| `Mask` | `string` | The mask that the input value needs to match. |
| `UnmaskedCharacter` | `char` | The placeholder character for when no input has been given yet. |

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/MaskedBehaviorPage.xaml).

## API

You can find the source code for `MaskedBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/MaskedBehavior.cs).