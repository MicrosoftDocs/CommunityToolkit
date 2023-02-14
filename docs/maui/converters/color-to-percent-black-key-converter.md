---
title: ColorToPercentBlackKeyConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToPercentBlackKeyConverter is a one way converter that allows users to convert an incoming Color to the black key component as a value between 0 and 1."
ms.date: 04/15/2022
---

# ColorToPercentBlackKeyConverter

The `ColorToPercentBlackKeyConverter` is a one way converter that allows users to convert an incoming `Color` to the **key** component as a value between 0 and 1.

The `Convert` method returns the **key** component as a value between 0 and 1 from the supplied `value`.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `ColorToPercentBlackKeyConverter` to display the **key** component of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToPercentBlackKeyConverter

The `ColorToPercentBlackKeyConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToPercentBlackKeyConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToPercentBlackKeyConverter x:Key="ColorToPercentBlackKeyConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
         <Label Text="The key component is:" />

         <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToPercentBlackKeyConverter}}" />
     </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToPercentBlackKeyConverter` can be used as follows in C#:

```csharp
class ColorToPercentBlackKeyConverterPage : ContentPage
{
    public ColorToPercentBlackKeyConverterPage()
    {
        var label = new Label();

 		label.SetBinding(
 			Label.TextProperty,
 			new Binding(
 				nameof(ViewModel.MyFavoriteColor),
 				converter: new ColorToPercentBlackKeyConverter()));

 		Content = new VerticalStackLayout
 		{
 			Children =
 			{
 				new Label { Text = "The key component is:" },
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

class ColorToPercentBlackKeyConverterPage : ContentPage
{
    public ColorToPercentBlackKeyConverterPage()
    {
        Content = new VerticalStackLayout
        {
            Children =
            {
                new Label()
                    .Text("The key component is:"),
                new Label()
                    .Bind(
                        Label.TextProperty,
                        static (ViewModel vm) => vm.MyFavoriteColor,
                        converter: new ColorToPercentBlackKeyConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToPercentBlackKeyConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToComponentConverter.shared.cs).
