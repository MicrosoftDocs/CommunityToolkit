---
title: ColorToPercentKeyConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToPercentKeyConverter is a one way converter that allows users to convert an incoming Color to the black key component as a value between 0 and 1."
ms.date: 04/15/2022
---

# ColorToPercentKeyConverter

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `ColorToPercentKeyConverter` is a one way converter that allows users to convert an incoming `Color` to the **key** component as a value between 0 and 1.

The `Convert` method returns the **key** component as a value between 0 and 1 from the supplied `value`.

The `ConvertBack` method is not supported.

## Syntax

The following examples will show how to use the `ColorToPercentKeyConverter` to display the **key** component of a specific `Color`.

### XAML

The `ColorToPercentKeyConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToPercentKeyConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToPercentKeyConverter x:Key="ColorToPercentKeyConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
         <Label Text="The key component is:" />

         <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToPercentKeyConverter}}" />
     </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToPercentKeyConverter` can be used as follows in C#:

```csharp
class ColorToPercentKeyConverterPage : ContentPage
{
    public ColorToPercentKeyConverterPage()
    {
        var label = new Label();

 		label.SetBinding(
 			Label.TextProperty,
 			new Binding(
 				nameof(ViewModel.MyFavoriteColor),
 				converter: new ColorToPercentKeyConverter()));

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

class ColorToPercentKeyConverterPage : ContentPage
{
    public ColorToPercentKeyConverterPage()
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
 						nameof(ViewModel.MyFavoriteColor),
 						converter: new ColorToPercentKeyConverter())
 			}
 		};
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToPercentKeyConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToComponentConverter.shared.cs).
