---
title: MultiConverter - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The MultiConverter converts an incoming value using all of the incoming converters in sequence."
ms.date: 03/02/2022
---

# MultiConverter

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `MultiConverter` converts an incoming value using all of the incoming converters in sequence.

## Syntax

### XAML

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
                <toolkit:IsNotEqualConverter />
            </toolkit:MultiConverter>
            <x:Array x:Key="MultiParams"
                     Type="{x:Type toolkit:MultiConverterParameter}">
                <toolkit:MultiConverterParameter
                    ConverterType="{x:Type toolkit:TextCaseConverter}"
                    Value="{x:Static toolkit:TextCaseType.Upper}" />
                <toolkit:MultiConverterParameter
                    ConverterType="{x:Type toolkit:IsNotEqualConverter}"
                    Value="MAUI" />
            </x:Array>
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="{Binding EnteredName, Converter={StaticResource MyMultiConverter}, ConverterParameter={StaticResource MultiParams}, Mode=OneWay}" />

</ContentPage>
```

This sample demonstrates how to use the `MultiConverter` with the [`IsNotEqualConverter`](is-not-equal-converter.md) and the [`TextCaseConverter`](text-case-converter.md). It converts the entered text to Upper Case and checks that it is Not Equal to the string 'MAUI'.
            

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/MultiConverterPage.xaml).

## API

You can find the source code for `MultiConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/MultiConverter.shared.cs).
