---
title: ColorToHslaStringConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToHslaStringConverter is a one way converter that allows users to convert a Color value binding to its HSLA string equivalent."
ms.date: 11/15/2026
---

# ColorToHslaStringConverter

The `ColorToHslaStringConverter` is a one way converter that allows users to convert a `Color` value binding to its HSLA `string` equivalent in the format: **HSLA(hue,saturation,lightness,alpha)** where **hue** will be a value between 0 and 360, **saturation** and **lightness** will be a value between 0% and 100%, and **alpha** will be a value between 0 and 1 (e.g. **HSLA(360,100%,50%,1)** for `Colors.Red`.

The `Convert` method returns the supplied `Color` `value` converted to its HSLA `string` equivalent.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Culture

In a binding, the converter formats the percentages and the alpha value with the binding's `ConverterCulture`, or with `CurrentUICulture` when `ConverterCulture` isn't set. For example, `de-DE` writes `100 %` with a space before the `%` sign, and `tr-TR` writes `%100`. The alpha value `0.5` is `0,5` in `de-DE`.

Set `ConverterCulture` to `InvariantCulture` for the documented format, for example `HSLA(360,100%,50%,0.5)` for `Colors.Red` with an alpha of 0.5:

```xaml
<!-- xmlns:globalization="clr-namespace:System.Globalization;assembly=System.Runtime" -->
<Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToHslaStringConverter}, ConverterCulture={x:Static globalization:CultureInfo.InvariantCulture}}" />
```

Calling `ConvertFrom` directly without a culture, or with `null`, returns the same invariant format.

> [!IMPORTANT]
> **Behavior change after v17.0.0:** called directly with no culture, or with `null`, the converter now returns the invariant format. Through v17.0.0 it used `CultureInfo.CurrentCulture`. Bindings still use `ConverterCulture`, or `CurrentUICulture`. Passing `CultureInfo.InvariantCulture`, directly or through a binding, now returns `100%`, where .NET's invariant culture writes `100 %`.

## Syntax

The following examples will show how to use the `ColorToHslaStringConverter` to display the HSLA equivalent string of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToHslaStringConverter

The `ColorToHslaStringConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToHslaStringConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToHslaStringConverter x:Key="ColorToHslaStringConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Label Text="My favourite Color is:" />

        <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToHslaStringConverter}}" />
    </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToHslaStringConverter` can be used as follows in C#:

```csharp
class ColorToHslaStringConverterPage : ContentPage
{
    public ColorToHslaStringConverterPage()
    {
        var label = new Label();

        label.SetBinding(
            Label.TextProperty,
            new Binding(
                static (ViewModel vm) => vm.MyFavoriteColor,
                converter: new ColorToHslaStringConverter()));

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

class ColorToHslaStringConverterPage : ContentPage
{
    public ColorToHslaStringConverterPage()
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
                        converter: new ColorToHslaStringConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToHslaStringConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToStringConverter.shared.cs).
