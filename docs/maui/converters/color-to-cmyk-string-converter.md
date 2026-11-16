---
title: ColorToCmykStringConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ColorToCmykStringConverter is a one way converter that allows users to convert a Color value binding to its CMYK string equivalent."
ms.date: 11/15/2026
---

# ColorToCmykStringConverter

The `ColorToCmykStringConverter` is a one way converter that allows users to convert a `Color` value binding to its CMYK `string` equivalent in the format: **CMYK(cyan,magenta,yellow,key)** where **cyan**, **magenta**, **yellow** and **key** will be a value between 0% and 100% (e.g. **CMYK(0%,100%,100%,0%)** for `Colors.Red`.

The `Convert` method returns the supplied `Color` `value` converted to its CMYK `string` equivalent.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Culture

In a binding, the converter formats the percentages with the binding's `ConverterCulture`, or with `CurrentUICulture` when `ConverterCulture` isn't set. For example, `de-DE` writes `100 %` with a space before the `%` sign, and `tr-TR` writes `%100`.

Set `ConverterCulture` to `InvariantCulture` for the documented format, for example `CMYK(0%,100%,100%,0%)` for `Colors.Red`:

```xaml
<!-- xmlns:globalization="clr-namespace:System.Globalization;assembly=System.Runtime" -->
<Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToCmykStringConverter}, ConverterCulture={x:Static globalization:CultureInfo.InvariantCulture}}" />
```

Calling `ConvertFrom` directly without a culture, or with `null`, returns the same invariant format.

> [!IMPORTANT]
> **Behavior change after v17.0.0:** called directly with no culture, or with `null`, the converter now returns the invariant format. Through v17.0.0 it used `CultureInfo.CurrentCulture`. Bindings still use `ConverterCulture`, or `CurrentUICulture`. Passing `CultureInfo.InvariantCulture`, directly or through a binding, now returns `100%`, where .NET's invariant culture writes `100 %`.

## Syntax

The following examples will show how to use the `ColorToCmykStringConverter` to display the CMYK equivalent string of a specific `Color`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ColorToCmykStringConverter

The `ColorToCmykStringConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ColorToCmykStringConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ColorToCmykStringConverter x:Key="ColorToCmykStringConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Label Text="My favourite Color is:" />

        <Label Text="{Binding MyFavoriteColor, Converter={StaticResource ColorToCmykStringConverter}}" />
    </VerticalStackLayout>

</ContentPage>
```

### C#

The `ColorToCmykStringConverter` can be used as follows in C#:

```csharp
class ColorToCmykStringConverterPage : ContentPage
{
    public ColorToCmykStringConverterPage()
    {
        var label = new Label();

        label.SetBinding(
            Label.TextProperty,
            new Binding(
                static (ViewModel vm) => vm.MyFavoriteColor,
                converter: new ColorToCmykStringConverter()));

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

class ColorToCmykStringConverterPage : ContentPage
{
    public ColorToCmykStringConverterPage()
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
                        converter: new ColorToCmykStringConverter())
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ColorsConverterPage.xaml).

## API

You can find the source code for `ColorToCmykStringConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ColorToStringConverter.shared.cs).
