---
title: IsNotEqualConverter - .NET MAUI Community Toolkit
author: bijington
description: "The IsNotEqualConverter is a one way converter that returns a bool indicating whether the binding value is not equal to another specified value."
ms.date: 03/02/2022
---

# IsNotEqualConverter

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `IsNotEqualConverter` is a one way converter that returns a `bool` indicating whether the binding value is not equal to another specified value.

The `Convert` method returns `true` when the binding `value` is **not equal** to the supplied `ConverterParameter`.

The `ConvertBack` method is not supported. For the opposite behavior see the [`IsEqualConverter`](is-equal-converter.md).

## Syntax

### XAML

The `IsNotEqualConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.IsNotEqualConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:IsNotEqualConverter x:Key="IsNotEqualConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="The value is not equal to 100"
           IsVisible="{Binding MyValue, Converter={StaticResource IsNotEqualConverter}, ConverterParameter=100}" />

</ContentPage>
```

### C#

The `IsNotEqualConverter` can be used as follows in C#:

```csharp

class IsNotEqualConverterPage : ContentPage
{
    public IsNotEqualConverterPage()
    {
        var label = new Label { Text = "The value is not equal to 100" };

		label.SetBinding(
			Label.IsVisibleProperty,
			new Binding(
				nameof(ViewModels.MyValue),
				converter: new IsNotEqualConverter(),
				converterParameter: 100));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class IsNotEqualConverterPage : ContentPage
{
    public IsNotEqualConverterPage()
    {
        Content = new Label { Text = "The value is not equal to 100" }
            .Bind(
                Label.IsVisibleProperty,
                nameof(ViewModel.MyValue),
                converter: new IsNotEqualConverter(),
                converterParameter: 100);
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IsNotEqualConverterPage.xaml).

## API

You can find the source code for `IsNotEqualConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IsNotEqualConverter.shared.cs).
