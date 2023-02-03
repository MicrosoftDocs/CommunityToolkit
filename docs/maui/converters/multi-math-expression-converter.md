---
title: MultiMathExpressionConverter - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The MultiMathExpressionConverter is a converter for multiple math expressions."
ms.date: 05/16/2022
---

# MultiMathExpressionConverter

The `MultiMathExpressionConverter` is a converter that allows users to perform various math operations with multiple values through using a `MultiBinding`.

The `Convert` calculates the expression string defined in the `ConverterParameter` with multiple variables and returns a `double` result.

The values that are passed in to the converter will be named `x?` where ? is the order in which it is defined in the `MultiBinding`, any other variable names in the expression will be ignored. For example to express the calculation of `P = V * I` (power = volts * amps) the following can be written:

```xaml
<Label.Text>
    <MultiBinding Converter="{StaticResource MultiMathExpressionConverter}" ConverterParameter="x0 * x1">
        <Binding Path="Volts" />
        <Binding Path="Amps" />
    </MultiBinding>
</Label.Text>
```

## Syntax

The following examples show how to add a `Label` that will show the result of `x0 + x1 + x2` where the `x` values will be supplied in the order of the `MultiBinding` definitions.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the MultiMathExpressionConverter

The `MultiMathExpressionConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.MultiMathExpressionConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:MultiMathExpressionConverter x:Key="MultiMathExpressionConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label HorizontalOptions="Center">
        <Label.Text>
            <MultiBinding Converter="{StaticResource MultiMathExpressionConverter}" ConverterParameter="x0 + x1 + x2">
                <Binding Path="X0" />
                <Binding Path="X1" />
                <Binding Path="X2" />
            </MultiBinding>
        </Label.Text>
    </Label>

</ContentPage>
```

### C#

The `MultiMathExpressionConverter` can be used as follows in C#:

```csharp
class MultiMathExpressionConverterPage : ContentPage
{
    public MultiMathExpressionConverterPage()
    {
        var label = new Label
        {
            HorizontalOptions = LayoutOptions.Center
        };

        label.SetBinding(
            Label.TextProperty,
            new MultiBinding
            {
                Converter = new MultiMathExpressionConverter(),
                ConverterParameter = "x0 + x1 + x2",
                Bindings = new List<BindingBase>
                {
                    new Binding(nameof(ViewModel.X0)),
                    new Binding(nameof(ViewModel.X1)),
                    new Binding(nameof(ViewModel.X2))
                }
            });

        Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
class MultiMathExpressionConverterPage : ContentPage
{
    public MultiMathExpressionConverterPage()
    {
        Content = new Label()
            .CenterHorizontal()
            .Bind(
                Label.TextProperty,
                new List<BindingBase>
                {
                    new Binding(nameof(ViewModel.X0)),
                    new Binding(nameof(ViewModel.X1)),
                    new Binding(nameof(ViewModel.X2))
                },
                converter: new MultiMathExpressionConverter(),
                converterParameter: "x0 + x1 + x2");
    }
}
```

[!INCLUDE [Math Expression operations](../includes/math-expression-operations.md)]

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/MultiMathExpressionConverterPage.xaml).

## API

You can find the source code for `MultiMathExpressionConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/MultiMathExpressionConverter/MultiMathExpressionConverter.shared.cs).
