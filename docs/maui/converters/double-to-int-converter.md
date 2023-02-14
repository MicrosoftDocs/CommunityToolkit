---
title: DoubleToIntConverter - .NET MAUI Community Toolkit
author: bijington
description: "The DoubleToIntConverter is a converter that allows users to convert an incoming double value to an int and vice-versa."
ms.date: 03/09/2022
---

# DoubleToIntConverter

The `DoubleToIntConverter` is a converter that allows users to convert an incoming `double` value to an `int` and vice-versa. Optionally the user can provide a multiplier to the conversion through the `Ratio` property.

The `Convert` method returns the supplied `value` converted to an `int` and multiplied by a ratio.

The `ConvertBack` method returns the supplied `value` converted to a `double` and divided by a ratio.

> [!NOTE]
> Note that the ratio can be supplied in the following ways:
> 1. as the `ConverterParameter` in the converter binding,
> 1. as the `Ratio` property on the converter.
> 
> Note that the `ConverterParameter` option will take precedence over the `Ratio` property.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the DoubleToIntConverter

The `DoubleToIntConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.DoubleToIntConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:DoubleToIntConverter x:Key="DoubleToIntConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="{Binding MyValue, Converter={StaticResource DoubleToIntConverter}}" />

</ContentPage>
```

### C#

The `DoubleToIntConverter` can be used as follows in C#:

```csharp
class DoubleToIntConverterPage : ContentPage
{
    public DoubleToIntConverterPage()
    {
        var label = new Label();

		label.SetBinding(
			Label.TextProperty,
			new Binding(
				nameof(ViewModel.MyValue),
				converter: new DoubleToIntConverter()));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class DoubleToIntConverterPage : ContentPage
{
    public DoubleToIntConverterPage()
    {
        Content = new Label()
            .Bind(
                Label.TextProperty,
                static (ViewModel vm) => vm.MyValue,
                converter: new DoubleToIntConverter());
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| Ratio | `int` | The multiplier to apply during the conversion. |

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/DoubleToIntConverterPage.xaml).

## API

You can find the source code for `DoubleToIntConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/DoubleToIntConverter.shared.cs).
