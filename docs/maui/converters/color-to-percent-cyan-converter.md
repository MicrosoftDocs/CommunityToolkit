---
title: ColorToPercentCyanConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToPercentCyanConverter is a one way converter that allows users to convert an incoming Color to the cyan component as a value between 0 and 1."
ms.date: 04/15/2022
---

# ColorToPercentCyanConverter

The `ColorToPercentCyanConverter` is a one way converter that allows users to convert an incoming `Color` to the **cyan** component as a value between 0 and 1.

The `Convert` method returns the **cyan** component as a value between 0 and 1 from the supplied `value`.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `ColorToPercentCyanConverter` to display the **cyan** component of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToPercentCyanConverter

The `ColorToPercentCyanConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToPercentCyanConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToPercentCyanConverter x:Key="ColorToPercentCyanConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
         <Label Text="The cyan component is:" />

         <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToPercentCyanConverter}}" />
     </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToPercentCyanConverter` can be used as follows in C#:

```csharp
class ColorToPercentCyanConverterPage : ContentPage
{
    public ColorToPercentCyanConverterPage()
    {
        var label = new Label();

 		label.SetBinding(
 			Label.TextProperty,
 			new Binding(
 				nameof(ViewModel.MyFavoriteColor),
 				converter: new ColorToPercentCyanConverter()));

 		Content = new VerticalStackLayout
 		{
 			Children =
 			{
 				new Label { Text = "The cyan component is:" },
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

class ColorToPercentCyanConverterPage : ContentPage
{
    public ColorToPercentCyanConverterPage()
    {
        Content = new VerticalStackLayout
        {
            Children =
            {
                new Label()
                    .Text("The cyan component is:"),
                new Label()
                    .Bind(
                        Label.TextProperty,
                        static (ViewModel vm) => vm.MyFavoriteColor,
                        converter: new ColorToPercentCyanConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToPercentCyanConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToComponentConverter.shared.cs).
