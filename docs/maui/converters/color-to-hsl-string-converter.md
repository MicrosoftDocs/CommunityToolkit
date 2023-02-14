---
title: ColorToHslStringConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToHslStringConverter is a one way converter that allows users to convert a Color value binding to its HSL string equivalent."
ms.date: 04/15/2022
---

# ColorToHslStringConverter

The `ColorToHslStringConverter` is a one way converter that allows users to convert a `Color` value binding to its HSL `string` equivalent in the format: **HSL(hue,saturation,lightness)** where **hue** will be a value between 0 and 360, and **saturation** and **lightness** will be a value between 0% and 100% (e.g. **HSL(0,100%,50%)** for `Colors.Red`.

The `Convert` method returns the supplied `Color` `value` converted to its HSL `string` equivalent.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `ColorToHslStringConverter` to display the HSL equivalent string of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToHslStringConverter

The `ColorToHslStringConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToHslStringConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToHslStringConverter x:Key="ColorToHslStringConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Label Text="My favourite Color is:" />

        <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToHslStringConverter}}" />
    </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToHslStringConverter` can be used as follows in C#:

```csharp
class ColorToHslStringConverterPage : ContentPage
{
    public ColorToHslStringConverterPage()
    {
        var label = new Label();

	label.SetBinding(
		Label.TextProperty,
		new Binding(
			nameof(ViewModel.MyFavoriteColor),
			converter: new ColorToHslStringConverter()));

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

class ColorToHslStringConverterPage : ContentPage
{
    public ColorToHslStringConverterPage()
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
                        converter: new ColorToHslStringConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToHslStringConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToStringConverter.shared.cs).
