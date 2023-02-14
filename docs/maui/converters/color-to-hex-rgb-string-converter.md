---
title: ColorToHexRgbStringConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToHexRgbStringConverter is a one way converter that allows users to convert a Color value binding to its RGB hexadecimal string equivalent."
ms.date: 04/15/2022
---

# ColorToHexRgbStringConverter

The `ColorToHexRgbStringConverter` is a that allows users to convert a `Color` value binding to its RGB hexadecimal `string` equivalent in the format: **#redgreenblue** where **red**, **green** and **blue** will be a value between 0 and FF (e.g. **#FF0000** for `Colors.Red`.

The `Convert` method returns the supplied `Color` `value` converted to its RGB hexadecimal `string` equivalent.

The `ConvertBack` method returns the RGB hexadecimal `string` `value` converted to a `Color`.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `ColorToHexRgbStringConverter` to display the RGB hexadecimal equivalent string of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToHexRgbStringConverter

The `ColorToHexRgbStringConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToHexRgbStringConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToHexRgbStringConverter x:Key="ColorToHexRgbStringConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Label Text="My favourite Color is:" />

        <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToHexRgbStringConverter}}" />
    </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToHexRgbStringConverter` can be used as follows in C#:

```csharp
class ColorToHexRgbStringConverterPage : ContentPage
{
    public ColorToHexRgbStringConverterPage()
    {
        var label = new Label();

	label.SetBinding(
		Label.TextProperty,
		new Binding(
			nameof(ViewModel.MyFavoriteColor),
			converter: new ColorToHexRgbStringConverter()));

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

class ColorToHexRgbStringConverterPage : ContentPage
{
    public ColorToHexRgbStringConverterPage()
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
                        converter: new ColorToHexRgbStringConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToHexRgbStringConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToStringConverter.shared.cs).
