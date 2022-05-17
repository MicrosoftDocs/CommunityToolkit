---
title: MathExpressionConverter - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The MathExpressionConverter is a converter that allows users to perform various math operations."
ms.date: 03/16/2022
---

# MathExpressionConverter

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `MathExpressionConverter` is a converter that allows users to perform various math operations. This works with a single binding value, if you require multiple values through a `MultiBinding` then see [`MultiMathExpressionConverter`](multi-math-expression-converter.md)

The `Convert` calculates the incoming expression string with one variable and returns a `double` result.

## Syntax

### XAML

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
				nameof(ViewModels.MyValue),
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
                nameof(ViewModel.MyValue),
                converter: new MathExpressionConverter(),
                converterParameter: "x/2"));
    }
}
```

## Available operations

- "+"
- "-"
- "*"
- "/"
- "%"
- "abs"
- "acos"
- "asin"
- "atan"
- "atan2"
- "ceiling"
- "cos"
- "cosh"
- "exp"
- "floor"
- "ieeeremainder"
- "log"
- "log10"
- "max"
- "min"
- "pow"
- "round"
- "sign"
- "sin"
- "sinh"
- "sqrt"
- "tan"
- "tanh"
- "truncate"
- "^"
- "pi"
- "e"

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/MathExpressionConverterPage.xaml).

## API

You can find the source code for `MathExpressionConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/MathExpressionConverter/MathExpressionConverter.shared.cs).
