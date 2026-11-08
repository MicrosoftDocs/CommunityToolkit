---
title: MathExpressionConverter - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The MathExpressionConverter is a converter that allows users to perform various math operations."
ms.date: 11/10/2026
---

# MathExpressionConverter

The `MathExpressionConverter` is a converter that allows users to perform various math operations. This works with a single `Binding` value, if you require multiple values through a `MultiBinding` then see [`MultiMathExpressionConverter`](multi-math-expression-converter.md)

The `Convert` calculates the expression string defined in the `ConverterParameter` with one variable and returns a `double` result.

The value that is passed in to the converter will be named `x`. In order to refer to this value inside the expression you must use `x` (e.g. `x / 2` will divide the incoming value by 2). Any other variable names in the expression will be ignored.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Culture

The expression syntax doesn't depend on the culture. Numbers in the expression always use `.` as the decimal separator, and function and constant names are case-insensitive in every culture, so `IF` and `PI` also work in Turkish.

String inputs are parsed with the culture passed to the converter, the binding's `ConverterCulture`, which defaults to `CultureInfo.CurrentUICulture`. Under `tr-TR` or `de-DE`, the string `"3.5"` is read as `35`, because `.` is the group separator. A quoted string in the expression, and the `str()` and `len()` functions, use that culture too.

Bind numbers as numbers, or set `ConverterCulture` to `CultureInfo.InvariantCulture` when the text is invariant.

## Syntax

The following examples show how to add a `Label` that will show the result of `x / 2` where `x` will have the value of `MyValue`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the MathExpressionConverter

The `MathExpressionConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.MathExpressionConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:MathExpressionConverter x:Key="MathExpressionConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="{Binding MyValue, Converter={StaticResource MathExpressionConverter}, ConverterParameter='x/2'}" />

</ContentPage>
```

### C#

The `MathExpressionConverter` can be used as follows in C#:

```csharp
class MathExpressionConverterPage : ContentPage
{
    public MathExpressionConverterPage()
    {
        var label = new Label();

        label.SetBinding(
            Label.TextProperty,
            new Binding(
                static (ViewModels vm) => vm.MyValue,
                converter: new MathExpressionConverter(),
                converterParameter: "x/2"));

        Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class MathExpressionConverterPage : ContentPage
{
    public MathExpressionConverterPage()
    {
        Content = new Label()
            .Bind(
                Label.TextProperty,
                static (ViewModel vm) => vm.MyValue,
                converter: new MathExpressionConverter(),
                converterParameter: "x/2");
    }
}
```

[!INCLUDE [Math Expression operations](../includes/math-expression-operations.md)]

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/MathExpressionConverterPage.xaml).

## API

You can find the source code for `MathExpressionConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/MathExpressionConverter/MathExpressionConverter.shared.cs).
