---
title: ColorToRgbStringConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToRgbStringConverter is a one way converter that allows users to convert a Color value binding to its RGB string equivalent."
ms.date: 04/15/2022
---

# ColorToRgbStringConverter

The `ColorToRgbStringConverter` is a one way converter that allows users to convert a `Color` value binding to its RGB `string` equivalent in the format: **RGB(red,green,blue)** where **red**, **green** and **blue** will be a value between 0 and 255 (e.g. **RGB(255,0,0)** for `Colors.Red`.

The `Convert` method returns the supplied `Color` `value` converted to its RGB `string` equivalent.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `ColorToRgbStringConverter` to display the RGB equivalent string of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToRgbStringConverter

The `ColorToRgbStringConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToRgbStringConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToRgbStringConverter x:Key="ColorToRgbStringConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Label Text="My favourite Color is:" />

        <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToRgbStringConverter}}" />
    </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToRgbStringConverter` can be used as follows in C#:

```csharp
class ColorToRgbStringConverterPage : ContentPage
{
    public ColorToRgbStringConverterPage()
    {
        var label = new Label();

	label.SetBinding(
		Label.TextProperty,
		new Binding(
			nameof(ViewModel.MyFavoriteColor),
			converter: new ColorToRgbStringConverter()));

	Content = new VerticalStackLayout
	{
		Children =
		{
			new Label { Text = "My favourite Color is:" },
			label
		}
	};
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class ColorToRgbStringConverterPage : ContentPage
{
    public ColorToRgbStringConverterPage()
    {
        Content = new VerticalStackLayout
        {
            Children =
            {
                new Label()
                    .Text("My favourite Color is:"),
                new Label()
                    .Bind(
                        Label.TextProperty,
                        static (ViewModel vm) => vm.MyFavoriteColor,
                        converter: new ColorToRgbStringConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToRgbStringConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToStringConverter.shared.cs).
