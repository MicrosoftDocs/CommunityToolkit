---
title: ColorToHexRgbaStringConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToHexRgbaStringConverter is a one way converter that allows users to convert a Color value binding to its RGBA hexadecimal string equivalent."
ms.date: 04/15/2022
---

# ColorToHexRgbaStringConverter

The `ColorToHexRgbaStringConverter` is a that allows users to convert a `Color` value binding to its RGBA hexadecimal `string` equivalent in the format: **#redgreenbluealpha** where **red**, **green**, **blue** and **alpha** will be a value between 0 and FF (e.g. **#FF0000FF** for `Colors.Red`.

The `Convert` method returns the supplied `Color` `value` converted to its RGB hexadecimal `string` equivalent.

The `ConvertBack` method returns the RGB hexadecimal `string` `value` converted to a `Color`.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `ColorToHexRgbaStringConverter` to display the RGB hexadecimal equivalent string of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToHexRgbaStringConverter

The `ColorToHexRgbaStringConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToHexRgbaStringConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToHexRgbaStringConverter x:Key="ColorToHexRgbaStringConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Label Text="My favourite Color is:" />

        <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToHexRgbaStringConverter}}" />
    </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToHexRgbaStringConverter` can be used as follows in C#:

```csharp
class ColorToHexRgbaStringConverterPage : ContentPage
{
    public ColorToHexRgbaStringConverterPage()
    {
        var label = new Label();

	label.SetBinding(
		Label.TextProperty,
		new Binding(
			nameof(ViewModel.MyFavoriteColor),
			converter: new ColorToHexRgbaStringConverter()));

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

class ColorToHexRgbaStringConverterPage : ContentPage
{
    public ColorToHexRgbaStringConverterPage()
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
                        converter: new ColorToHexRgbaStringConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToHexRgbaStringConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToStringConverter.shared.cs).
