---
title: VariableMultiValueConverter - .NET MAUI Community Toolkit
author: bijington
description: "The VariableMultiValueConverter is a converter that allows users to convert multiple bool value bindings to a single bool."
ms.date: 05/22/2022
---

# VariableMultiValueConverter

The `VariableMultiValueConverter` is a converter that allows users to convert `bool` values via a `MultiBinding` to a single `bool`. It does this by enabling them to specify whether All, Any, None or a specific number of values are true as specified in ConditionType.

The `Convert` method returns the supplied `values` converted to an overall `bool` result based on the `ConditionType` defined.

The `ConvertBack` method will only return a result if the `ConditionType` is set to `MultiBindingCondition.All`.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples show how to make a `Label` invisible based when at least 2 of the values in a `MultiBinding` evaluate to true.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the VariableMultiValueConverter

The `VariableMultiValueConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.VariableMultiValueConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:VariableMultiValueConverter 
                x:Key="VariableMultiValueConverter"
                ConditionType="LessThan"
                Count="2" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="At least 2 toppings must be selected.">
        <Label.IsVisible>
            <MultiBinding Converter="{StaticResource VariableMultiValueConverter}">
                <Binding Path="IsCheeseSelected" />
                <Binding Path="IsHamSelected" />
                <Binding Path="IsPineappleSelected" />
            </MultiBinding>
        </Label.IsVisible>
    </Label>

</ContentPage>
```

### C#

The `VariableMultiValueConverter` can be used as follows in C#:

```csharp

class VariableMultiValueConverterPage : ContentPage
{
    public VariableMultiValueConverterPage()
    {
        var label = new Label
        {
            Text = "At least 2 toppings must be selected."
        };

        label.SetBinding(
            Label.IsVisibleProperty,
            new MultiBinding
            {
                Converter = new VariableMultiValueConverter
                {
                    ConditionType = MultiBindingCondition.LessThan,
                    Count = 2
                },
                Bindings = new List<BindingBase>
                {
                    new Binding(nameof(ViewModel.IsCheeseSelected)),
                    new Binding(nameof(ViewModel.IsHamSelected)),
                    new Binding(nameof(ViewModel.IsPineappleSelected))
                }
            });

        Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class VariableMultiValueConverterPage : ContentPage
{
    public VariableMultiValueConverterPage()
    {
        Content = new Label()
            .Text("At least 2 toppings must be selected.")
            .Bind(
                Label.IsVisibleProperty,
                new List<BindingBase>
                {
                    new Binding(nameof(ViewModel.IsCheeseSelected)),
                    new Binding(nameof(ViewModel.IsHamSelected)),
                    new Binding(nameof(ViewModel.IsPineappleSelected))
                },
                converter: new VariableMultiValueConverter
                {
                    ConditionType = MultiBindingCondition.LessThan,
                    Count = 2
                });
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| ConditionType | `MultiBindingCondition` | Indicates how many values should be `true` out of the provided boolean values in the `MultiBinding`. |
| Count | `int` | The number of values that should be true when using `ConditionType` of `GreaterThan`, `LessThan` or `Exact`. |

### MultiBindingCondition

The `MultiBindingCondition` enumeration defines the following members:

- `None` - None of the values should be true.
- `All` - All of the values should be true.
- `Any` - Any of the values should be true.
- `Exact` - The exact number as configured in the `Count` property should be true.
- `GreaterThan` - Greater that the number as configured in the `Count` property should be true.
- `LessThan` - Less than the number as configured in the `Count` property should be true.

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/VariableMultiValueConverterPage.xaml).

## API

You can find the source code for `VariableMultiValueConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/VariableMultiValueConverter.shared.cs).
