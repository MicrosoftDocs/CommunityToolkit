---
title: ColorToByteRedConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToByteRedConverter is a one way converter that allows users to convert an incoming Color to the red component as a value between 0 and 255."
ms.date: 04/15/2022
---

# ColorToByteRedConverter

The `ColorToByteRedConverter` is a one way converter that allows users to convert an incoming `Color` to the **red** component as a value between 0 and 255.

The `Convert` method returns the **red** component as a value between 0 and 255 from the supplied `value`.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `ColorToByteRedConverter` to display the **red** component of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToByteRedConverter

The `ColorToByteRedConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToByteRedConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToByteRedConverter x:Key="ColorToByteRedConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
         <Label Text="The red component is:" />

         <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToByteRedConverter}}" />
     </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToByteRedConverter` can be used as follows in C#:

```csharp
class ColorToByteRedConverterPage : ContentPage
{
    public ColorToByteRedConverterPage()
    {
        var label = new Label();

 		label.SetBinding(
 			Label.TextProperty,
 			new Binding(
 				nameof(ViewModel.MyFavoriteColor),
 				converter: new ColorToByteRedConverter()));

 		Content = new VerticalStackLayout
 		{
 			Children =
 			{
 				new Label { Text = "The red component is:" },
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

class ColorToByteRedConverterPage : ContentPage
{
    public ColorToByteRedConverterPage()
    {
        Content = new VerticalStackLayout
        {
            Children =
            {
                new Label()
                    .Text("The red component is:"),
                new Label()
                    .Bind(
                        Label.TextProperty,
                        static (ViewModel vm) => vm.MyFavoriteColor,
                        converter: new ColorToByteRedConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToByteRedConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToComponentConverter.shared.cs).
