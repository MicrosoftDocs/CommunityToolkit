---
title: IsEqualConverter - .NET MAUI Community Toolkit
author: bijington
description: "The IsEqualConverter is a one way converter that returns a bool indicating whether the binding value is equal to another specified value."
ms.date: 03/02/2022
---

# IsEqualConverter

The `IsEqualConverter` is a one way converter that returns a `bool` indicating whether the binding value is equal to another specified value.

The `Convert` method returns `true` when the binding `value` is **equal** to the supplied `ConverterParameter`.

The `ConvertBack` method is not supported. For the opposite behavior see the [`IsNotEqualConverter`](is-not-equal-converter.md).

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the IsEqualConverter

The `IsEqualConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.IsEqualConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:IsEqualConverter x:Key="IsEqualConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="The value is equal to 100"
           IsVisible="{Binding MyValue, Converter={StaticResource IsEqualConverter}, ConverterParameter=100}" />

</ContentPage>
```

### C#

The `IsEqualConverter` can be used as follows in C#:

```csharp

class IsEqualConverterPage : ContentPage
{
    public IsEqualConverterPage()
    {
        var label = new Label { Text = "The value is equal to 100" };

		label.SetBinding(
			Label.IsVisibleProperty,
			new Binding(
				nameof(ViewModels.MyValue),
				converter: new IsEqualConverter(),
				converterParameter: 100));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class IsEqualConverterPage : ContentPage
{
    public IsEqualConverterPage()
    {
        Content = new Label { Text = "The value is equal to 100" }
            .Bind(
                Label.IsVisibleProperty,
                static (ViewModel vm) => vm.MyValue,
                converter: new IsEqualConverter(),
                converterParameter: 100);
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IsEqualConverterPage.xaml).

## API

You can find the source code for `IsEqualConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IsEqualConverter.shared.cs).
