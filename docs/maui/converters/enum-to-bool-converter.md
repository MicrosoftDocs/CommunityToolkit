---
title: EnumToBoolConverter - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The EnumToBoolConverter is a converter that allows you to convert a Enum to corresponding bool type."
ms.date: 05/04/2022
---

# EnumToBoolConverter

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `EnumToBoolConverter` is a converter that allows you to convert a standard `Enum` to corresponding `bool` type. It is useful when binding a collection of values representing an enumeration type to a boolean control property like `IsVisible`.

## Syntax

### XAML

The `EnumToBoolConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyLittleApp.MainPage">
    <ContentPage.Resources>
         <ResourceDictionary>
             <toolkit:EnumToBoolConverter x:Key="MobileConverter">
                <toolkit:EnumToBoolConverter.TrueValues>
                    <vm:MyDevicePlatform>Android</vm:MyDevicePlatform>
                    <vm:MyDevicePlatform>iOS</vm:MyDevicePlatform>
                </mct:EnumToBoolConverter.TrueValues>
            </mct:EnumToBoolConverter>
         </ResourceDictionary>
    </ContentPage.Resources>

    <Picker ItemsSource="{Binding Platforms}" SelectedItem="{Binding SelectedPlatform}" />
    <Label IsVisible="{Binding SelectedPlatform, Converter={StaticResource MobileConverter}}" Text="I am visible when the Picker value is Android or iOS."/>

</ContentPage>
```

It is also possible to pass the converter parameter:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyLittleApp.MainPage">
    <ContentPage.Resources>
         <ResourceDictionary>
             <toolkit:EnumToBoolConverter x:Key="PlatformConverter" />
         </ResourceDictionary>
    </ContentPage.Resources>

    <Picker ItemsSource="{Binding Platforms}" SelectedItem="{Binding SelectedPlatform}" />
    <Label IsVisible="{Binding SelectedPlatform, Converter={StaticResource PlatformConverter}, ConverterParameter={x:Static vm:MyDevicePlatform.Tizen}}" Text="I am visible when the Picker value is Tizen."/>

</ContentPage>
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| TrueValues | `IList<Enum>` | Enum values, that converts to `true` (optional).  |


## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/EnumToBoolConverterPage.xaml).

## API

You can find the source code for `EnumToBoolConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/EnumToBoolConverter.shared.cs).
