---
title: NumericValidationBehavior - .NET MAUI Community Toolkit
author: bijington
description: "The NumericValidationBehavior is a Behavior that allows the user to determine if text input is a valid numeric value."
ms.date: 10/02/2026
---

# NumericValidationBehavior

The `NumericValidationBehavior` is a `Behavior` that allows the user to determine if text input is a valid numeric value. For example, an `Entry` control can be styled differently depending on whether a valid or an invalid numeric input is provided.

[!INCLUDE [important note on bindings within behaviors](../includes/behavior-bindings.md)]

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

## Interval validation

The `Interval` property restricts valid input to multiples of a given value. For example, when `Interval` is `0.25`, the values `1.5` and `1.75` are valid but `1.6` isn't. When `Interval` is `null`, which is the default, no interval restriction is applied.

The following example only considers multiples of 5 between 0 and 100 to be valid, such as 0, 5, 10, and 100:

```xaml
<Entry Keyboard="Numeric" Placeholder="Multiple of 5">
    <Entry.Behaviors>
        <toolkit:NumericValidationBehavior
            InvalidStyle="{StaticResource InvalidEntryStyle}"
            ValidStyle="{StaticResource ValidEntryStyle}"
            Flags="ValidateOnValueChanged"
            MinimumValue="0.0"
            MaximumValue="100.0"
            Interval="5.0" />
    </Entry.Behaviors>
</Entry>
```

The equivalent C# code is:

```csharp
var numericValidationBehavior = new NumericValidationBehavior
{
    InvalidStyle = invalidStyle,
    ValidStyle = validStyle,
    Flags = ValidationFlags.ValidateOnValueChanged,
    MinimumValue = 0.0,
    MaximumValue = 100.0,
    Interval = 5.0
};
```

When using the `Interval` property, keep the following in mind:

- Multiples are counted from zero in both directions (..., -10, -5, 0, 5, 10, ...), not from `MinimumValue`. For example, when `Interval` is `5` and `MinimumValue` is `3`, the values `5` and `10` are valid but `3` and `8` aren't.
- A value must also satisfy `MinimumValue`, `MaximumValue`, `MinimumDecimalPlaces`, and `MaximumDecimalPlaces` to be valid.
- A negative `Interval` behaves like its absolute value. For example, an `Interval` of `-5` is the same as an `Interval` of `5`.
- An `Interval` of `0` isn't the same as `null`. Because `0` is the only multiple of `0`, only a value of `0` is valid.
- `Interval` must be `null` or a finite number. Assigning `double.NaN`, `double.PositiveInfinity`, or `double.NegativeInfinity` doesn't throw an exception. Instead, the assignment is ignored and `Interval` keeps its previous value.

> [!NOTE]
> Most decimal fractions can't be stored exactly in a `double`, so a small rounding tolerance is applied when checking for multiples. For example, `0.3` is considered a multiple of `0.1`. The tolerance assumes that `Interval` is the `double` closest to the intended value, such as `0.1` written in XAML or C#. An `Interval` that carries extra rounding error, such as the result of `1.1 - 1.0` (`0.10000000000000009`) or the `float` value `0.1f` (`0.10000000149011612`), rejects values such as `0.1` and `0.3`. Round such a value before assigning it, for example by using `Math.Round(interval, 2)`.
>
> Because a `double` holds only about 15 significant digits, very large values can be considered multiples even when they aren't exact multiples. For example, when `Interval` is `0.3`, `1000000000000000` is considered valid even though the nearest multiple is `999999999999999.9`.

> [!TIP]
> When a value fails validation, `NumericValidationBehavior` writes the reason using `System.Diagnostics.Trace`. For example, entering `7` when `Interval` is `5` writes `NumericValidationBehavior: "7" is invalid because 7 is not a multiple of Interval (5)`.

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| `Interval` | `double?` | The interval that a valid numeric value must be a multiple of. For example, an `Interval` of `0.25` allows `1.5` and `1.75` but not `1.6`. When `null` (the default), no interval restriction is applied. For more information, see [Interval validation](#interval-validation). |
| `MaximumDecimalPlaces` | `int` | The maximum number of decimal places that will be allowed. |
| `MinimumDecimalPlaces` | `int` | The minimum number of decimal places that will be allowed. |
| `MaximumValue` | `double` | The maximum numeric value that will be allowed. |
| `MinimumValue` | `double` | The minimum numeric value that will be allowed. |

[!INCLUDE [common validation properties](../includes/validation-behavior.md)]

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/NumericValidationBehaviorPage.xaml).

## API

You can find the source code for `NumericValidationBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/Validators/NumericValidationBehavior.shared.cs).