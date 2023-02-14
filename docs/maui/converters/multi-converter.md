---
title: MultiConverter - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The MultiConverter converts an incoming value using all of the incoming converters in sequence."
ms.date: 03/02/2022
---

# MultiConverter

The `MultiConverter` converts an incoming value using all of the incoming converters in sequence. The order in which the converters are used is based on the order they are defined.

## Syntax

This sample demonstrates how to use the `MultiConverter` with the [`IsEqualConverter`](is-equal-converter.md) and the [`TextCaseConverter`](text-case-converter.md). It converts the entered text to **upper case** and then checks that it is **equal** to the string 'MAUI', this will result in a `boolean` value and is bound to the `IsVisible` property on a `Label` control.

This example makes use of the `MultiConverterParameter` which allows for the ConverterParameter to be defined for the type of converter the `MultiConverterParameter` is set to.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the MultiConverter

The `MultiConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.MultiConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:MultiConverter x:Key="MyMultiConverter">
                <toolkit:TextCaseConverter />
                <toolkit:IsEqualConverter />
            </toolkit:MultiConverter>
            <x:Array x:Key="MultiParams"
                     Type="{x:Type toolkit:MultiConverterParameter}">
                <toolkit:MultiConverterParameter
                    ConverterType="{x:Type toolkit:TextCaseConverter}"
                    Value="{x:Static toolkit:TextCaseType.Upper}" />
                <toolkit:MultiConverterParameter
                    ConverterType="{x:Type toolkit:IsEqualConverter}"
                    Value="MAUI" />
            </x:Array>
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label IsVisible="{Binding EnteredName, Converter={StaticResource MyMultiConverter}, ConverterParameter={StaticResource MultiParams}, Mode=OneWay}" 
           Text="Well done you guessed the magic word!"/>

</ContentPage>
```

### C#

The `MultiConverter` can be used as follows in C#:

```csharp
class MultiConverterPage : ContentPage
{
    public MultiConverterPage()
    {
        var label = new Label { Text = "Well done you guessed the magic word!" };

        var converter = new MultiConverter
        {
            new TextCaseConverter(),
            new IsEqualConverter()
        };

        var parameters = new List<MultiConverterParameter>
        {
            new MultiConverterParameter { ConverterType = typeof(TextCaseConverter), Value = TextCaseType.Upper },
            new MultiConverterParameter { ConverterType = typeof(IsEqualConverter), Value = "MAUI" },
        };

        label.SetBinding(
            Label.IsVisibleProperty,
            new Binding(
                nameof(ViewModels.EnteredName),
                converter: converter,
                converterParameter: parameters));

        Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
class MultiConverterPage : ContentPage
{
    public MultiConverterPage()
    {
        var converter = new MultiConverter
        {
            new TextCaseConverter(),
            new IsEqualConverter()
        };

        var parameters = new List<MultiConverterParameter>
        {
            new MultiConverterParameter { ConverterType = typeof(TextCaseConverter), Value = TextCaseType.Upper },
            new MultiConverterParameter { ConverterType = typeof(IsEqualConverter), Value = "MAUI" },
        };

        Content = new Label()
            .Text("Well done you guessed the magic word!")
            .Bind(
                Label.IsVisibleProperty,
                static (ViewModel vm) => vm.EnteredName,
                converter: converter,
                converterParameter: parameters);
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/MultiConverterPage.xaml).

## API

You can find the source code for `MultiConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/MultiConverter.shared.cs).
