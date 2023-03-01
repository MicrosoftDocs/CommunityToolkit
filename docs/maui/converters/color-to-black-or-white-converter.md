---
title: ColorToBlackOrWhiteConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToBlackOrWhiteConverter is a one way converter that allows users to convert an incoming Color to a monochrome value of either Colors.Black or Colors.White."
ms.date: 03/24/2022
---

# ColorToBlackOrWhiteConverter

The `ColorToBlackOrWhiteConverter` is a one way converter that allows users to convert an incoming `Color` to a monochrome value of either `Colors.Black` or `Colors.White`.

The `Convert` method returns the supplied `value` converted to either `Colors.Black` or `Colors.White` based on whether the supplied `value` is considered dark or not. A `Color` is considered when its red, green and blue components each average less than 127.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToBlackOrWhiteConverter

The `ColorToBlackOrWhiteConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToBlackOrWhiteConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToBlackOrWhiteConverter x:Key="ColorToBlackOrWhiteConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="The Text is showing in monochrome"
           TextColor="{Binding AppTextColor, Converter={StaticResource ColorToBlackOrWhiteConverter}}" />

</ContentPage>
```

### C#

The `ColorToBlackOrWhiteConverter` can be used as follows in C#:

```csharp
class ColorToBlackOrWhiteConverterPage : ContentPage
{
    public ColorToBlackOrWhiteConverterPage()
    {
        var label = new Label { Text = "The Text is showing in monochrome" };

		label.SetBinding(
			Label.TextColorProperty,
			new Binding(
				nameof(ViewModels.AppTextColor),
				converter: new ColorToBlackOrWhiteConverter()));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class ColorToBlackOrWhiteConverterPage : ContentPage
{
    public ColorToBlackOrWhiteConverterPage()
    {
        Content = new Label { Text = "The Text is showing in monochrome" }
            .Bind(
                Label.TextColorProperty,
                static (ViewModel vm) => vm.AppTextColor,
                converter: new ColorToBlackOrWhiteConverter());
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToBlackOrWhiteConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToColorConverters.shared.cs).
