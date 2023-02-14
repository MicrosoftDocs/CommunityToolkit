---
title: ColorToCmykStringConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToCmykStringConverter is a one way converter that allows users to convert a Color value binding to its CMYK string equivalent."
ms.date: 04/15/2022
---

# ColorToCmykStringConverter

The `ColorToCmykStringConverter` is a one way converter that allows users to convert a `Color` value binding to its CMYK `string` equivalent in the format: **CMYK(cyan,magenta,yellow,key)** where **cyan**, **magenta**, **yellow** and **key** will be a value between 0% and 100% (e.g. **CMYK(0%,100%,100%,0%)** for `Colors.Red`.

The `Convert` method returns the supplied `Color` `value` converted to its CMYK `string` equivalent.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `ColorToCmykStringConverter` to display the CMYK equivalent string of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToCmykStringConverter

The `ColorToCmykStringConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToCmykStringConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToCmykStringConverter x:Key="ColorToCmykStringConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Label Text="My favourite Color is:" />

        <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToCmykStringConverter}}" />
    </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToCmykStringConverter` can be used as follows in C#:

```csharp
class ColorToCmykStringConverterPage : ContentPage
{
    public ColorToCmykStringConverterPage()
    {
        var label = new Label();

	label.SetBinding(
		Label.TextProperty,
		new Binding(
			nameof(ViewModel.MyFavoriteColor),
			converter: new ColorToCmykStringConverter()));

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

class ColorToCmykStringConverterPage : ContentPage
{
    public ColorToCmykStringConverterPage()
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
                        converter: new ColorToCmykStringConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToCmykStringConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToStringConverter.shared.cs).
