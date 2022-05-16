---
title: MultiMathExpressionConverter - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The MultiMathExpressionConverter is a converter for multiple math expressions."
ms.date: 03/16/2022
---

# MultiMathExpressionConverter

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `MultiMathExpressionConverter` is a converter for multiple math expressions.

The `Convert` calculates the incoming expression string with multiple variables and returns a `double` result.

## Syntax

### XAML

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

    <Label HorizontalOptions="Center" >
        <Label.FormattedText>
            <FormattedString>
                <Span Text="x0 + x1 + x2 = "/>
                <Span>
                    <Span.Text>
                        <MultiBinding Converter="{StaticResource MultiMathExpressionConverter}" ConverterParameter="x0 + x1 + x2">
                            <Binding Path="X0" />
                            <Binding Path="X1" />
                            <Binding Path="X2" />
                        </MultiBinding>
                    </Span.Text>
                </Span>
            </FormattedString>
        </Label.FormattedText>
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
        var label = new Label();

		label.SetBinding(
			Label.TextProperty,
			new MultiBinding()
			{
				Converter = new MultiMathExpressionConverter(),
				ConverterParameter = "x0 + x1 + x2",
				Bindings = new List<BindingBase>()
				{
					new Binding("X0"),
					new Binding("X1"),
					new Binding("X2")
				}
			});

		Content = label;
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

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/MultiMathExpressionConverterPage.xaml).

## API

You can find the source code for `MultiMathExpressionConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/MultiMathExpressionConverter/MultiMathExpressionConverter.shared.cs).
