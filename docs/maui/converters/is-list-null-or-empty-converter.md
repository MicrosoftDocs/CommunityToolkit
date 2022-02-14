---
title: .NET MAUI IsListNullOrEmptyConverter
author: bijington
description: "The IsListNullOrEmptyConverter is a one way converter that converts IEnumerable to a bool value."
ms.date: 02/11/2022
---

# IsListNullOrEmptyConverter

[!INCLUDE [docs under construction](includes/preview-note.md)]

The `IsListNullOrEmptyConverter` is a one way converter that converts `IEnumerable` to a `bool` value. 

The `Convert` method returns `true` when `null` or an empty `IEnumerable` is passed in or `false` otherwise.

The `ConvertBack` method is not supported. For the opposite behavior see the [`IsListNotNullOrEmptyConverter`](is-list-not-null-or-empty-converter.md).

## Syntax

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:mct="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.IsListNullOrEmptyConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <mct:IsListNullOrEmptyConverter x:Key="IsListNullOrEmptyConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>

        <Label Text="{Binding StringItemSource, Converter={StaticResource IsListNullOrEmptyConverter}}"
               TextColor="Black" />

    </VerticalStackLayout>

</ContentPage>
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IsListNullOrEmptyConverterPage.xaml).

## API

You can find the source code for `IsListNullOrEmptyConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IsListNullOrEmptyConverter.cs).