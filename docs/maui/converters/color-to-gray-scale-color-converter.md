---
title: ColorToGrayScaleColorConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToGrayScaleColorConverter is a one way converter that allows users to convert an incoming Color to a grayscale Color."
ms.date: 03/24/2022
---

# ColorToGrayScaleColorConverter

The `ColorToGrayScaleColorConverter` is a one way converter that allows users to convert an incoming `Color` to a grayscale `Color`.

The `Convert` method returns the supplied `value` converted to a grayscale `Color`.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToGrayScaleColorConverter

The `ColorToGrayScaleColorConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToGrayScaleColorConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToGrayScaleColorConverter x:Key="ColorToGrayScaleColorConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="The Text is showing in grayscale"
           TextColor="{Binding AppTextColor, Converter={StaticResource ColorToGrayScaleColorConverter}}" />

</ContentPage>
```

### C#

The `ColorToGrayScaleColorConverter` can be used as follows in C#:

```csharp
class ColorToGrayScaleColorConverterPage : ContentPage
{
    public ColorToGrayScaleColorConverterPage()
    {
        var label = new Label { Text = "The Text is showing in grayscale" };

		label.SetBinding(
			Label.TextColorProperty,
			new Binding(
				nameof(ViewModels.AppTextColor),
				converter: new ColorToGrayScaleColorConverter()));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class ColorToGrayScaleColorConverterPage : ContentPage
{
    public ColorToGrayScaleColorConverterPage()
    {
        Content = new Label { Text = "The Text is showing in grayscale" }
            .Bind(
                Label.TextColorProperty,
                static (ViewModel vm) => vm.AppTextColor,
                converter: new ColorToGrayScaleColorConverter());
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToGrayScaleColorConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToColorConverters.shared.cs).
