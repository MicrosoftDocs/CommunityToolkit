---
title: ImageResourceConverter - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The ImageResourceConverter is a converter that converts embedded image resource ID to its ImageSource."
ms.date: 05/04/2022
---

# ImageResourceConverter

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `ImageResourceConverter` is a converter that converts embedded image resource ID to its ImageSource.

## Syntax

### XAML

The `ImageResourceConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ImageResourceConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ImageResourceConverter x:Key="ImageResourceConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Image Source="{Binding MyImageResource, Converter={StaticResource ImageResourceConverter}}" />

</ContentPage>
```

`MyImageResource` may look like this: `MyAssemblyName.Resources.Embedded.Image.png`

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ImageResourceConverterPage.xaml).

## API

You can find the source code for `ImageResourceConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ImageResourceConverter.shared.cs).
