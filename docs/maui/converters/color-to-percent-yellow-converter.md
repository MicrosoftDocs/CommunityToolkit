---
title: ColorToPercentYellowConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToPercentYellowConverter is a one way converter that allows users to convert an incoming Color to the yellow component as a value between 0 and 1."
ms.date: 04/15/2022
---

# ColorToPercentYellowConverter

The `ColorToPercentYellowConverter` is a one way converter that allows users to convert an incoming `Color` to the **yellow** component as a value between 0 and 1.

The `Convert` method returns the **yellow** component as a value between 0 and 1 from the supplied `value`.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `ColorToPercentYellowConverter` to display the **yellow** component of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToPercentYellowConverter

The `ColorToPercentYellowConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToPercentYellowConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToPercentYellowConverter x:Key="ColorToPercentYellowConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
         <Label Text="The yellow component is:" />

         <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToPercentYellowConverter}}" />
     </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToPercentYellowConverter` can be used as follows in C#:

```csharp
class ColorToPercentYellowConverterPage : ContentPage
{
    public ColorToPercentYellowConverterPage()
    {
        var label = new Label();

 		label.SetBinding(
 			Label.TextProperty,
 			new Binding(
 				nameof(ViewModel.MyFavoriteColor),
 				converter: new ColorToPercentYellowConverter()));

 		Content = new VerticalStackLayout
 		{
 			Children =
 			{
 				new Label { Text = "The yellow component is:" },
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

class ColorToPercentYellowConverterPage : ContentPage
{
    public ColorToPercentYellowConverterPage()
    {
        Content = new VerticalStackLayout
        {
            Children =
            {
                new Label()
                    .Text("The yellow component is:"),
                new Label()
                    .Bind(
                        Label.TextProperty,
                        static (ViewModel vm) => vm.MyFavoriteColor,
                        converter: new ColorToPercentYellowConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToPercentYellowConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToComponentConverter.shared.cs).
