---
title: IntToBoolConverter - .NET MAUI Community Toolkit
author: bijington
description: "The IntToBoolConverter is a converter that allows users to convert an incoming int value to a bool and vice-versa."
ms.date: 03/16/2022
---

# IntToBoolConverter

The `IntToBoolConverter` is a converter that allows users to convert an incoming `int` value to a `bool` and vice-versa.

The `Convert` method returns `false` if the supplied `value` is equal to `0` and `true` otherwise.

The `ConvertBack` method returns `1` if the supplied `value` is `true` and `0` otherwise.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the IntToBoolConverter

The `IntToBoolConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.IntToBoolConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:IntToBoolConverter x:Key="IntToBoolConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="The value is not zero."
           IsVisible="{Binding MyValue, Converter={StaticResource IntToBoolConverter}}" />

</ContentPage>
```

### C#

The `IntToBoolConverter` can be used as follows in C#:

```csharp
class IntToBoolConverterPage : ContentPage
{
    public IntToBoolConverterPage()
    {
        var label = new Label { Text = "The value is not zero." };

		label.SetBinding(
			Label.IsVisibleProperty,
			new Binding(
				nameof(ViewModels.MyValue),
				converter: new IntToBoolConverter()));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class IntToBoolConverterPage : ContentPage
{
    public IntToBoolConverterPage()
    {
        Content = new Label { Text = "The value is not zero." }
            .Bind(
                Label.IsVisibleProperty,
                static (ViewModel vm) => vm.MyValue,
                converter: new IntToBoolConverter());
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IntToBoolConverterPage.xaml).

## API

You can find the source code for `IntToBoolConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IntToBoolConverter.shared.cs).
