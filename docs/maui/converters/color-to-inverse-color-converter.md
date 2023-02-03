---
title: ColorToInverseColorConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToInverseColorConverter is a one way converter that allows users to convert an incoming Color to its inverse."
ms.date: 03/24/2022
---

# ColorToInverseColorConverter

The `ColorToInverseColorConverter` is a one way converter that allows users to convert an incoming `Color` to its inverse.

The `Convert` method returns the supplied `value` converted to its inverse.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToInverseColorConverter

The `ColorToInverseColorConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters. ColorToInverseColorConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToInverseColorConverter x:Key="ColorToInverseColorConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="This Text is the inverse of the Background"
           TextColor="{Binding Source={RelativeSource AncestorType={x:Type ContentPage}}, Path=BackgroundColor, Converter={StaticResource ColorToInverseColorConverter}}" />

</ContentPage>
```

### C#

The `ColorToInverseColorConverter` can be used as follows in C#:

```csharp
class ColorToInverseColorConverterPage : ContentPage
{
    public ColorToInverseColorConverterPage()
    {
        var label = new Label { Text = "This Text is the inverse of the Background" };

		label.SetBinding(
			Label.TextColorProperty,
			new Binding(
				nameof(ContentPage.BackgroundColor),
				converter: new ColorToInverseColorConverter(),
                source: this));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class ColorToInverseColorConverterPage : ContentPage
{
    public ColorToInverseColorConverterPage()
    {
        Content = new Label { Text = "This Text is the inverse of the Background" }
            .Bind(
                Label.TextColorProperty,
                nameof(ContentPage.BackgroundColor),
                converter: new ColorToInverseColorConverter(),
                source: this);
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToInverseColorConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToColorConverters.shared.cs).
