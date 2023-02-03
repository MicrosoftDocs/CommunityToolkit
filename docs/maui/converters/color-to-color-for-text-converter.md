---
title: ColorToColorForTextConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToColorForTextConverter is a one way converter that allows users to convert an incoming Color to a monochrome value of either Colors.Black or Colors.White based on whether it is determined as being dark for the human eye."
ms.date: 03/24/2022
---

# ColorToColorForTextConverter

The `ColorToColorForTextConverter` is a one way converter that allows users to convert an incoming `Color` to a monochrome value of either `Colors.Black` or `Colors.White` based on whether it is determined as being dark for the human eye.

The `Convert` method returns the supplied `value` converted to either `Colors.Black` or `Colors.White` based on whether the supplied `value` is considered dark for the human eye or not.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToColorForTextConverter

The `ColorToColorForTextConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToColorForTextConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToColorForTextConverter x:Key="ColorToColorForTextConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="The Text is showing in an optimum color against the background"
           TextColor="{Binding Source={RelativeSource AncestorType={x:Type ContentPage}}, Path=BackgroundColor, Converter={StaticResource ColorToColorForTextConverter}}" />

</ContentPage>
```

### C#

The `ColorToColorForTextConverter` can be used as follows in C#:

```csharp
class ColorToColorForTextConverterPage : ContentPage
{
    public ColorToColorForTextConverterPage()
    {
        var label = new Label { Text = "The Text is showing in an optimum color against the background" };

		label.SetBinding(
			Label.TextColorProperty,
			new Binding(
				nameof(ContentPage.BackgroundColor),
				converter: new ColorToColorForTextConverter(),
				source: this));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class ColorToColorForTextConverterPage : ContentPage
{
    public ColorToColorForTextConverterPage()
    {
        Content = new Label { Text = "The Text is showing in an optimum color against the background" }
            .Bind(
                Label.TextColorProperty,
                nameof(ContentPage.BackgroundColor),
                converter: new ColorToColorForTextConverter(),
                source: this);
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToColorForTextConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToColorConverters.shared.cs).
