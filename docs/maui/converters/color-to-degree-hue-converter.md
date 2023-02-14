---
title: ColorToDegreeHueConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToDegreeHueConverter is a one way converter that allows users to convert an incoming Color to the hue component as a value between 0 and 360."
ms.date: 04/15/2022
---

# ColorToDegreeHueConverter

The `ColorToDegreeHueConverter` is a one way converter that allows users to convert an incoming `Color` to the **hue** component as a value between 0 and 360. Hue is a degree on the color wheel from 0 to 360. 0 is red, 120 is green, 240 is blue.

The `Convert` method returns the **hue** component as a value between 0 and 360 from the supplied `value`.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `ColorToDegreeHueConverter` to display the **hue** component of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToDegreeHueConverter

The `ColorToDegreeHueConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToDegreeHueConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToDegreeHueConverter x:Key="ColorToDegreeHueConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
         <Label Text="The hue component is:" />

         <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToDegreeHueConverter}}" />
     </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToDegreeHueConverter` can be used as follows in C#:

```csharp
class ColorToDegreeHueConverterPage : ContentPage
{
    public ColorToDegreeHueConverterPage()
    {
        var label = new Label();

 		label.SetBinding(
 			Label.TextProperty,
 			new Binding(
 				nameof(ViewModel.MyFavoriteColor),
 				converter: new ColorToDegreeHueConverter()));

 		Content = new VerticalStackLayout
 		{
 			Children =
 			{
 				new Label { Text = "The hue component is:" },
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

class ColorToDegreeHueConverterPage : ContentPage
{
    public ColorToDegreeHueConverterPage()
    {
        Content = new VerticalStackLayout
        {
            Children =
            {
                new Label()
                    .Text("The hue component is:"),
                new Label()
                    .Bind(
                        Label.TextProperty,
                        static (ViewModel vm) => vm.MyFavoriteColor,
                        converter: new ColorToDegreeHueConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToDegreeHueConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToComponentConverter.shared.cs).
