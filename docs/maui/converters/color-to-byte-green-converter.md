---
title: ColorToByteGreenConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToByteGreenConverter is a one way converter that allows users to convert an incoming Color to the green component as a value between 0 and 255."
ms.date: 04/15/2022
---

# ColorToByteGreenConverter

The `ColorToByteGreenConverter` is a one way converter that allows users to convert an incoming `Color` to the **green** component as a value between 0 and 255.

The `Convert` method returns the **green** component as a value between 0 and 255 from the supplied `value`.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `ColorToByteGreenConverter` to display the **green** component of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToByeGreenConverter

The `ColorToByteGreenConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToByteGreenConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToByteGreenConverter x:Key="ColorToByteGreenConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
         <Label Text="The green component is:" />

         <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToByteGreenConverter}}" />
     </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToByteGreenConverter` can be used as follows in C#:

```csharp
class ColorToByteGreenConverterPage : ContentPage
{
    public ColorToByteGreenConverterPage()
    {
        var label = new Label();

 		label.SetBinding(
 			Label.TextProperty,
 			new Binding(
 				nameof(ViewModel.MyFavoriteColor),
 				converter: new ColorToByteGreenConverter()));

 		Content = new VerticalStackLayout
 		{
 			Children =
 			{
 				new Label { Text = "The green component is:" },
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

class ColorToByteGreenConverterPage : ContentPage
{
    public ColorToByteGreenConverterPage()
    {
        Content = new VerticalStackLayout
        {
            Children =
            {
                new Label()
                    .Text("The green component is:"),
                new Label()
                    .Bind(
                        Label.TextProperty,
                        static (ViewModel vm) => vm.MyFavoriteColor,
                        converter: new ColorToByteGreenConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToByteGreenConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToComponentConverter.shared.cs).
