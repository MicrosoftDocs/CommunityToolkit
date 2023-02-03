---
title: NumericValidationBehavior - .NET MAUI Community Toolkit
author: bijington
description: "The NumericValidationBehavior is a Behavior that allows the user to determine if text input is a valid numeric value."
ms.date: 04/16/2022
---

# NumericValidationBehavior

The `NumericValidationBehavior` is a `Behavior` that allows the user to determine if text input is a valid numeric value. For example, an `Entry` control can be styled differently depending on whether a valid or an invalid numeric input is provided.

## Syntax

The following examples show how to add the `NumericValidationBehavior` to an `Entry` and change the `TextColor` when the number entered is considered invalid (not between 1 and 100).

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the NumericValidationBehavior

The `NumericValidationBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Behaviors.NumericValidationBehaviorPage">

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
            <toolkit:NumericValidationBehavior 
                InvalidStyle="{StaticResource InvalidEntryStyle}"
                ValidStyle="{StaticResource ValidEntryStyle}"
                Flags="ValidateOnValueChanged"
                MinimumValue="1.0"
                MaximumValue="100.0"
                MaximumDecimalPlaces="2" />
        </Entry.Behaviors>
    </Entry>

</ContentPage>
```

### C#

The `NumericValidationBehavior` can be used as follows in C#:

```csharp
class NumericValidationBehaviorPage : ContentPage
{
    public NumericValidationBehaviorPage()
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

        var numericValidationBehavior = new NumericValidationBehavior
        {
            InvalidStyle = invalidStyle,
            ValidStyle = validStyle,
            Flags = ValidationFlags.ValidateOnValueChanged,
            MinimumValue = 1.0,
            MaximumValue = 100.0,
            MaximumDecimalPlaces = 2
        };

        entry.Behaviors.Add(numericValidationBehavior);

        Content = entry;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class NumericValidationBehaviorPage : ContentPage
{
    public NumericValidationBehaviorPage()
    {
        Content = new Entry
        {
            Keyboard = Keyboard.Numeric
        }.Behaviors(new NumericValidationBehavior
        {
            InvalidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Red),
            ValidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Green),
            Flags = ValidationFlags.ValidateOnValueChanged,
            MinimumValue = 1.0,
            MaximumValue = 100.0,
            MaximumDecimalPlaces = 2
        });
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| `MaximumDecimalPlaces` | `double` | The maximum number of decimal places that will be allowed. |
| `MinimumDecimalPlaces` | `double` | The minimum number of decimal places that will be allowed. |
| `MaximumValue` | `double` | The maximum numeric value that will be allowed. |
| `MinimumValue` | `double` | The minimum numeric value that will be allowed. |

[!INCLUDE [common validation properties](../includes/validation-behavior.md)]

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/NumericValidationBehaviorPage.xaml).

## API

You can find the source code for `NumericValidationBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/Validators/NumericValidationBehavior.shared.cs).