---
title: ColorToHexArgbStringConverter - .NET MAUI Community Toolkit
author: cl2raul66
description: "The ColorToHexArgbStringConverter is a converter that allows users to convert a Color value binding to its ARGB hexadecimal string equivalent."
ms.date: 08/05/2024
---

# ColorToHexArgbStringConverter

The `ColorToHexArgbStringConverter` is a converter that allows users to convert a `Color` value binding to its ARGB hexadecimal `string` equivalent in the format: **#alpharedgreenblue** where **alpha**, **red**, **green**, and **blue** will be a value between 0 and FF (e.g., **#FFFF0000** for `Colors.Red`).

The `Convert` method returns the supplied `Color` `value` converted to its ARGB hexadecimal `string` equivalent.

The `ConvertBack` method returns the ARGB hexadecimal `string` `value` converted to a `Color`.

!INCLUDE [common converter properties]

## Syntax

The following examples will show how to use the `ColorToHexArgbStringConverter` to display the ARGB hexadecimal equivalent string of a specific `Color`.

### XAML

#### Including the XAML namespace

!INCLUDE [XAML usage guidance]

#### Using the ColorToHexArgbStringConverter

The `ColorToHexArgbStringConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToHexArgbStringConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToHexArgbStringConverter x:Key="ColorToHexArgbStringConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Label Text="My favorite color is:" />

        <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToHexArgbStringConverter}}" />
    </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToHexArgbStringConverter` can be used as follows in C#:

```csharp
class ColorToHexArgbStringConverterPage : ContentPage
{
    public ColorToHexArgbStringConverterPage()
    {
        var label = new Label();

	label.SetBinding(
		Label.TextProperty,
		new Binding(
			nameof(ViewModel.MyFavoriteColor),
			converter: new ColorToHexArgbStringConverter()));

	Content = new VerticalStackLayout
	{
		Children =
		{
			new Label { Text = "My favorite color is:" },
			label
		}
	};
    }
}
```

### C# Markup

Our `CommunityToolkit.Maui.Markup` package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class ColorToHexArgbStringConverterPage : ContentPage
{
    public ColorToHexArgbStringConverterPage()
    {
        Content = new VerticalStackLayout
        {
            Children =
            {
                new Label()
                    .Text("My favorite color is:"),
                new Label()
                    .Bind(
                        Label.TextProperty,
                        static (ViewModel vm) => vm.MyFavoriteColor,
                        converter: new ColorToHexArgbStringConverter())
            }
        };
    }
}
```

## Examples 

You can find an example of this converter in action in the .NET MAUI Community Toolkit Sample Application.

## API

You can find the source code for `ColorToHexArgbStringConverter` over on the .NET MAUI Community Toolkit GitHub repository.
