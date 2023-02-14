---
title: ColorToCmykaStringConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToCmykaStringConverter is a one way converter that allows users to convert a Color value binding to its CMYKA string equivalent."
ms.date: 04/15/2022
---

# ColorToCmykaStringConverter

The `ColorToCmykaStringConverter` is a one way converter that allows users to convert a `Color` value binding to its CMYKA `string` equivalent in the format: **CMYKA(cyan,magenta,yellow,key,alpha)** where **cyan**, **magenta**, **yellow** and **key** will be a value between 0% and 100%, and **alpha** will be a value between o and 1 (e.g. **CMYKA(0%,100%,100%,0%,1)** for `Colors.Red`.

The `Convert` method returns the supplied `Color` `value` converted to its CMYKA `string` equivalent.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `ColorToCmykaStringConverter` to display the CMYKA equivalent string of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToCmykaStringConverter

The `ColorToCmykaStringConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToCmykaStringConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToCmykaStringConverter x:Key="ColorToCmykaStringConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Label Text="My favourite Color is:" />

        <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToCmykaStringConverter}}" />
    </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToCmykaStringConverter` can be used as follows in C#:

```csharp
class ColorToCmykaStringConverterPage : ContentPage
{
    public ColorToCmykaStringConverterPage()
    {
        var label = new Label();

	label.SetBinding(
		Label.TextProperty,
		new Binding(
			nameof(ViewModel.MyFavoriteColor),
			converter: new ColorToCmykaStringConverter()));

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

class ColorToCmykaStringConverterPage : ContentPage
{
    public ColorToCmykaStringConverterPage()
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
                        converter: new ColorToCmykaStringConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToCmykaStringConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToStringConverter.shared.cs).
