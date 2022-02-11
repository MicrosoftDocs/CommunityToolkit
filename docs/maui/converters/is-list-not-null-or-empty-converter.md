---
title: .NET MAUI IsListNotNullOrEmptyConverter
author: bijington
description: "The IsListNotNullOrEmptyConverter is a one way converter that converts IEnumerable to a bool value."
ms.date: 02/11/2022
---

# IsListNotNullOrEmptyConverter

The `IsListNotNullOrEmptyConverter` is a one way converter that converts `IEnumerable` to a `bool` value. 

The `Convert` method returns `false` when `null` or an empty `IEnumerable` is passed in or `true` otherwise.

The `ConvertBack` method is not supported.

## Syntax

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:mct="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.IsListNotNullOrEmptyConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <mct:IsListNotNullOrEmptyConverter x:Key="IsListNotNullOrEmptyConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>

        <Label Text="{Binding StringItemSource, Converter={StaticResource IsListNotNullOrEmptyConverter}}"
               TextColor="Black" />

    </VerticalStackLayout>

</ContentPage>
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IsListNotNullOrEmptyConverterPage.xaml).

## API

You can find the source code for `IsListNotNullOrEmptyConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IsListNotNullOrEmptyConverter.cs).