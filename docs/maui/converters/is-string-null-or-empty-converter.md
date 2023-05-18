---
title: IsStringNullOrEmptyConverter - .NET MAUI Community Toolkit
author: bijington
description: "The IsStringNullOrEmptyConverter is a one way converter that returns a bool indicating whether the binding value is null or string.Empty."
ms.date: 03/30/2022
---

# IsStringNullOrEmptyConverter

The `IsStringNullOrEmptyConverter` is a one way converter that returns a `bool` indicating whether the binding value is null or `string.Empty`.

The `Convert` method returns `true` when the binding `value` is `null` or `string.Empty`.

The `ConvertBack` method is not supported. For the opposite behavior see the [`IsStringNotNullOrEmptyConverter`](is-string-not-null-or-empty-converter.md).

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the IsStringNullOrEmptyConverter

The `IsStringNullOrEmptyConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.IsStringNullOrEmptyConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:IsStringNullOrEmptyConverter x:Key="IsStringNullOrEmptyConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="A value is required"
           IsVisible="{Binding MyValue, Converter={StaticResource IsStringNullOrEmptyConverter}}" />

</ContentPage>
```

### C#

The `IsStringNullOrEmptyConverter` can be used as follows in C#:

```csharp
class IsStringNullOrEmptyConverterPage : ContentPage
{
    public IsStringNullOrEmptyConverterPage()
    {
        var label = new Label { Text = "A value is required" };

		label.SetBinding(
			Label.IsVisibleProperty,
			new Binding(
				nameof(ViewModels.MyValue),
				converter: new IsStringNullOrEmptyConverter()));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class IsStringNullOrEmptyConverterPage : ContentPage
{
    public IsStringNullOrEmptyConverterPage()
    {
        Content = new Label { Text = "A value is required" }
            .Bind(
                Label.IsVisibleProperty,
                static (ViewModel vm) => vm.MyValue,
                converter: new IsStringNullOrEmptyConverter());
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IsStringNullOrEmptyConverterPage.xaml).

## API

You can find the source code for `IsStringNullOrEmptyConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IsStringNullOrEmptyConverter.shared.cs).
