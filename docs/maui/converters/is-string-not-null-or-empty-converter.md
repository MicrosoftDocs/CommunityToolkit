---
title: IsStringNotNullOrEmptyConverter - .NET MAUI Community Toolkit
author: bijington
description: "The IsStringNotNullOrEmptyConverter is a one way converter that returns a bool indicating whether the binding value is not null and not an string.Empty."
ms.date: 03/30/2022
---

# IsStringNotNullOrEmptyConverter

The `IsStringNotNullOrEmptyConverter` is a one way converter that returns a `bool` indicating whether the binding value is not null and not an `string.Empty`.

The `Convert` method returns `true` when the binding `value` is **not** `null` and **not** an `string.Empty`.

The `ConvertBack` method is not supported. For the opposite behavior see the [`IsStringNullOrEmptyConverter`](is-string-null-or-empty-converter.md).

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the IsStringNotNullOrEmptyConverter

The `IsStringNotNullOrEmptyConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.IsStringNotNullOrEmptyConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:IsStringNotNullOrEmptyConverter x:Key="IsStringNotNullOrEmptyConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="A value has been entered"
           IsVisible="{Binding MyValue, Converter={StaticResource IsStringNotNullOrEmptyConverter}}" />

</ContentPage>
```

### C#

The `IsStringNotNullOrEmptyConverter` can be used as follows in C#:

```csharp
class IsStringNotNullOrEmptyConverterPage : ContentPage
{
    public IsStringNotNullOrEmptyConverterPage()
    {
        var label = new Label { Text = "A value has been entered" };

		label.SetBinding(
			Label.IsVisibleProperty,
			new Binding(
				nameof(ViewModels.MyValue),
				converter: new IsStringNotNullOrEmptyConverter()));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class IsStringNotNullOrEmptyConverterPage : ContentPage
{
    public IsStringNotNullOrEmptyConverterPage()
    {
        Content = new Label { Text = "A value has been entered" }
            .Bind(
                Label.IsVisibleProperty,
                static (ViewModel vm) => vm.MyValue,
                converter: new IsStringNotNullOrEmptyConverter());
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IsStringNotNullOrEmptyConverterPage.xaml).

## API

You can find the source code for `IsStringNotNullOrEmptyConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IsStringNotNullOrEmptyConverter.shared.cs).
