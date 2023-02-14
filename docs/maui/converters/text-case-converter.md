---
title: TextCaseConverter - .NET MAUI Community Toolkit
author: bijington
description: "The TextCaseConverter is a one way converter that allows users to convert the casing of an incoming string type binding."
ms.date: 03/02/2022
---

# TextCaseConverter

The `TextCaseConverter` is a one way converter that allows users to convert the casing of an incoming `string` type binding. The `Type` property is used to define what kind of casing will be applied to the string.

The `Convert` method returns the supplied `value` converted to the defined `TextCaseType`. Note that the `TextCaseType` can be supplied in the following ways:
1. as the `ConverterParameter` in the converter binding,
1. as the `Type` property on the converter.

Note that the `ConverterParameter` option will take precedence over the `Type` property.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the TextCaseConverter

The `TextCaseConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.TextCaseConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:TextCaseConverter x:Key="TextCaseConverter" Type="Upper" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="{Binding MyValue, Converter={StaticResource TextCaseConverter}}" />

</ContentPage>
```

### C#

The `TextCaseConverter` can be used as follows in C#:

```csharp

class TextCaseConverterPage : ContentPage
{
    public TextCaseConverterPage()
    {
        var label = new Label();

		label.SetBinding(
			Label.TextProperty,
			new Binding(
				nameof(ViewModels.MyValue),
				converter: new TextCaseConverter { Type = TextCaseType.Upper }));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class TextCaseConverterPage : ContentPage
{
    public TextCaseConverterPage()
    {
        Content = new Label()
            .Bind(
                Label.TextProperty,
                static (ViewModel vm) => vm.MyValue,
                converter: new TextCaseConverter { Type = TextCaseType.Upper });
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| Type | `TextCaseType` | The type of casing to apply to the `string` value. |

### TextCaseType

The `TextCaseType` enumeration defines the following members:

- `None` - Applies no specific formatting to the string.
- `Upper` - Applies upper case formatting to the string.
- `Lower` - Applies lower case formatting to the string.
- `FirstUpperRestLower` - Applies upper case formatting to the first character and then lower case formatting to the remaining string.

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/TextCaseConverterPage.xaml).

## API

You can find the source code for `TextCaseConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/TextCaseConverter.shared.cs).
