---
title: ColorToByteBlueConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToByteBlueConverter is a one way converter that allows users to convert an incoming Color to the blue component as a value between 0 and 255."
ms.date: 04/15/2022
---

# ColorToByteBlueConverter

The `ColorToByteBlueConverter` is a one way converter that allows users to convert an incoming `Color` to the **blue** component as a value between 0 and 255.

The `Convert` method returns the **blue** component as a value between 0 and 255 from the supplied `value`.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `ColorToByteBlueConverter` to display the **blue** component of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToByteBlueConverter

The `ColorToByteBlueConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToByteBlueConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToByteBlueConverter x:Key="ColorToByteBlueConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
         <Label Text="The blue component is:" />

         <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToByteBlueConverter}}" />
     </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToByteBlueConverter` can be used as follows in C#:

```csharp
class ColorToByteBlueConverterPage : ContentPage
{
    public ColorToByteBlueConverterPage()
    {
        var label = new Label();

 		label.SetBinding(
 			Label.TextProperty,
 			new Binding(
 				nameof(ViewModel.MyFavoriteColor),
 				converter: new ColorToByteBlueConverter()));

 		Content = new VerticalStackLayout
 		{
 			Children =
 			{
 				new Label { Text = "The blue component is:" },
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

class ColorToByteBlueConverterPage : ContentPage
{
    public ColorToByteBlueConverterPage()
    {
        Content = new VerticalStackLayout
        {
            Children =
            {
                new Label()
                    .Text("The blue component is:"),
                new Label()
                    .Bind(
                        Label.TextProperty,
                        static (ViewModel vm) => vm.MyFavoriteColor,
                        converter: new ColorToByteBlueConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToByteBlueConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToComponentConverter.shared.cs).
