---
title: IsStringNotNullOrWhiteSpaceConverter - .NET MAUI Community Toolkit
author: bijington
description: "The IsStringNotNullOrWhiteSpaceConverter is a one way converter that returns a bool indicating whether the binding value is not null, not an string.Empty and does not contain whitespace characters only."
ms.date: 03/30/2022
---

# IsStringNotNullOrWhiteSpaceConverter

The `IsStringNotNullOrWhiteSpaceConverter` is a one way converter that returns a `bool` indicating whether the binding value is not null, not an `string.Empty` and does not contain whitespace characters only.

The `Convert` method returns `true` when the binding `value` is **not** `null`, **not** an `string.Empty` and **does not** contain whitespace characters only.

The `ConvertBack` method is not supported. For the opposite behavior see the [`IsStringNullOrWhitespaceConverter`](is-string-null-or-whitespace-converter.md).

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the IsStringNotNullOrWhitespaceConverter

The `IsStringNotNullOrWhiteSpaceConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.IsStringNotNullOrWhiteSpaceConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:IsStringNotNullOrWhiteSpaceConverter x:Key="IsStringNotNullOrWhiteSpaceConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="A value has been entered"
           IsVisible="{Binding MyValue, Converter={StaticResource IsStringNotNullOrWhiteSpaceConverter}}" />

</ContentPage>
```

### C#

The `IsStringNotNullOrWhiteSpaceConverter` can be used as follows in C#:

```csharp
class IsStringNotNullOrWhiteSpaceConverterPage : ContentPage
{
    public IsStringNotNullOrWhiteSpaceConverterPage()
    {
        var label = new Label { Text = "A value has been entered" };

		label.SetBinding(
			Label.IsVisibleProperty,
			new Binding(
				nameof(ViewModels.MyValue),
				converter: new IsStringNotNullOrWhiteSpaceConverter()));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class IsStringNotNullOrWhiteSpaceConverterPage : ContentPage
{
    public IsStringNotNullOrWhiteSpaceConverterPage()
    {
        Content = new Label { Text = "A value has been entered" }
            .Bind(
                Label.IsVisibleProperty,
                static (ViewModel vm) => vm.MyValue,
                converter: new IsStringNotNullOrWhiteSpaceConverter());
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IsStringNotNullOrWhiteSpaceConverterPage.xaml).

## API

You can find the source code for `IsStringNotNullOrWhiteSpaceConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IsStringNotNullOrWhiteSpaceConverter.shared.cs).
