---
title: RequiredStringValidationBehavior - .NET MAUI Community Toolkit
author: bijington
description: "The RequiredStringValidationBehavior is a Behavior that allows the user to determine if text input is equal to specific text."
ms.date: 04/20/2022
---

# RequiredStringValidationBehavior

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `RequiredStringValidationBehavior` is a `Behavior` that allows the user to determine if text input is equal to specific text. For example, an `Entry` control can be styled differently depending on whether a valid or an invalid text input is provided.

## Syntax

The following examples show how to add the `RequiredStringValidationBehavior` to an `Entry` and change the `TextColor` based on whether the `RequiredString` has been entered.

### XAML

The `RequiredStringValidationBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.RequiredStringValidationBehaviorPage">

    <ContentPage.Resources>
        <Style x:Key="InvalidEntryStyle" TargetType="Entry">
            <Setter Property="TextColor" Value="Red" />
        </Style>
        <Style x:Key="ValidEntryStyle" TargetType="Entry">
            <Setter Property="TextColor" Value="Green" />
        </Style>
    </ContentPage.Resources>

    <Entry Keyboard="Numeric">
        <Entry.Behaviors>
            <toolkit:RequiredStringValidationBehavior 
                InvalidStyle="{StaticResource InvalidEntryStyle}"
                ValidStyle="{StaticResource ValidEntryStyle}"
                Flags="ValidateOnValueChanged"
                RequiredString="MAGIC ANSWER" />
        </Entry.Behaviors>
    </Entry>

</ContentPage>
```

### C#

The `RequiredStringValidationBehavior` can be used as follows in C#:

```csharp
class RequiredStringValidationBehaviorPage : ContentPage
{
    public RequiredStringValidationBehaviorPage()
    {
        var entry = new Entry
        {
            Keyboard = Keyboard.Numeric
        };

        var validStyle = new Style(typeof(Entry));
        validStyle.Setters.Add(new Setter
        {
            Property = Entry.TextColorProperty,
            Value = Colors.Green
        });

        var invalidStyle = new Style(typeof(Entry));
        invalidStyle.Setters.Add(new Setter
        {
            Property = Entry.TextColorProperty,
            Value = Colors.Red
        });

        var RequiredStringValidationBehavior = new RequiredStringValidationBehavior
        {
            InvalidStyle = invalidStyle,
            ValidStyle = validStyle,
            Flags = ValidationFlags.ValidateOnValueChanged,
            RequiredString = "MAGIC ANSWER"
        };

        entry.Behaviors.Add(RequiredStringValidationBehavior);

        Content = entry;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class RequiredStringValidationBehaviorPage : ContentPage
{
    public RequiredStringValidationBehaviorPage()
    {
        Content = new Entry
        {
            Keyboard = Keyboard.Numeric
        }.Behaviors(new RequiredStringValidationBehavior
        {
            InvalidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Red),
            ValidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Green),
            Flags = ValidationFlags.ValidateOnValueChanged,
            RequiredString = "MAGIC ANSWER"
        });
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| `ExactMatch` | `bool` | Determines whether the entered text must match the whole contents of the `RequiredString` property or simply contain the `RequiredString` property value.
| `RequiredString` | `string` | The string that will be compared to the value provided by the user. |

[!INCLUDE [common validation properties](../includes/validation-behavior.md)]

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/RequiredStringValidationBehaviorPage.xaml).

## API

You can find the source code for `RequiredStringValidationBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/RequiredStringValidationBehavior.cs).