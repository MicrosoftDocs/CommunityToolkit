---
title: ColorToRgbaStringConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToRgbaStringConverter is a converter that allows users to convert a Color value binding to its RGBA string equivalent."
ms.date: 11/15/2026
---

# ColorToRgbaStringConverter

The `ColorToRgbaStringConverter` is a converter that allows users to convert a `Color` value binding to its RGBA `string` equivalent in the format: **RGBA(red,green,blue,alpha)** where **red**, **green** and **blue** will be a value between 0 and 255, and **alpha** is a value between 0 and 1 (e.g. **RGBA(255,0,0,1)** for `Colors.Red`.

The `Convert` method returns the supplied `Color` `value` converted to its RGBA `string` equivalent.

The `ConvertBack` method returns the RGBA `string` `value` converted to a `Color`.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Culture

In a binding, the converter formats the alpha value with the binding's `ConverterCulture`, or with `CurrentUICulture` when `ConverterCulture` isn't set. In a culture that uses a comma as the decimal separator, such as `de-DE`, an alpha value of 0.5 is written as `0,5`: `RGBA(255,0,0,0,5)`.

Set `ConverterCulture` to `InvariantCulture` for the documented format, for example `RGBA(255,0,0,0.5)` for `Colors.Red` with an alpha of 0.5:

```xaml
<!-- xmlns:globalization="clr-namespace:System.Globalization;assembly=System.Runtime" -->
<Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToRgbaStringConverter}, ConverterCulture={x:Static globalization:CultureInfo.InvariantCulture}}" />
```

Called directly, `ConvertFrom` without a culture, or with `null`, returns the same invariant format.

When it converts back, the converter reads strings in the documented format (`RGBA(255,0,0,0.5)`) in every culture. It also reads a comma-decimal alpha, such as `RGBA(255,0,0,0,5)`, using the culture that it is given. With no culture, or `null`, it uses `CurrentCulture`, so strings that v17.0.0 wrote on a comma-decimal machine still convert back.

> [!IMPORTANT]
> **Behavior change after v17.0.0:** called directly with no culture, or with `null`, the converter now returns the invariant format. Through v17.0.0 it used `CultureInfo.CurrentCulture`, so on a comma-decimal machine it returned `RGBA(255,0,0,0,5)`, which `Color.Parse` can't read back. Bindings are unchanged: they still use `ConverterCulture`, or `CurrentUICulture`.

## Syntax

The following examples will show how to use the `ColorToRgbaStringConverter` to display the RGBA equivalent string of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToRgbaStringConverter

The `ColorToRgbaStringConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToRgbaStringConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToRgbaStringConverter x:Key="ColorToRgbaStringConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Label Text="My favourite Color is:" />

        <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToRgbaStringConverter}}" />
    </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToRgbaStringConverter` can be used as follows in C#:

```csharp
class ColorToRgbaStringConverterPage : ContentPage
{
    public ColorToRgbaStringConverterPage()
    {
        var label = new Label();

        label.SetBinding(
            Label.TextProperty,
            new Binding(
                static (ViewModel vm) => vm.MyFavoriteColor,
                converter: new ColorToRgbaStringConverter()));

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

class ColorToRgbaStringConverterPage : ContentPage
{
    public ColorToRgbaStringConverterPage()
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
                        converter: new ColorToRgbaStringConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToRgbaStringConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToStringConverter.shared.cs).
