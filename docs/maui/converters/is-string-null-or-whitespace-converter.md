---
title: IsStringNullOrWhiteSpaceConverter - .NET MAUI Community Toolkit
author: bijington
description: "The IsStringNullOrWhiteSpaceConverter is a one way converter that returns a bool indicating whether the binding value is null or string.Empty or contains whitespace characters only."
ms.date: 03/30/2022
---

# IsStringNullOrWhiteSpaceConverter

The `IsStringNullOrWhiteSpaceConverter` is a one way converter that returns a `bool` indicating whether the binding value is null, `string.Empty` or contains whitespace characters only.

The `Convert` method returns `true` when the binding `value` is `null`, `string.Empty` or contains whitespace characters only.

The `ConvertBack` method is not supported. For the opposite behavior see the [`IsStringNotNullOrWhiteSpaceConverter`](is-string-not-null-or-whitespace-converter.md).

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the IsStringNullOrWhitespaceConverter

The `IsStringNullOrWhiteSpaceConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.IsStringNullOrWhiteSpaceConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:IsStringNullOrWhiteSpaceConverter x:Key="IsStringNullOrWhiteSpaceConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="A value is required"
           IsVisible="{Binding MyValue, Converter={StaticResource IsStringNullOrWhiteSpaceConverter}}" />

</ContentPage>
```

### C#

The `IsStringNullOrWhiteSpaceConverter` can be used as follows in C#:

```csharp
class IsStringNullOrWhiteSpaceConverterPage : ContentPage
{
    public IsStringNullOrWhiteSpaceConverterPage()
    {
        var label = new Label { Text = "A value is required" };

		label.SetBinding(
			Label.IsVisibleProperty,
			new Binding(
				nameof(ViewModels.MyValue),
				converter: new IsStringNullOrWhiteSpaceConverter()));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class IsStringNullOrWhiteSpaceConverterPage : ContentPage
{
    public IsStringNullOrWhiteSpaceConverterPage()
    {
        Content = new Label { Text = "A value is required" }
            .Bind(
                Label.IsVisibleProperty,
                static (ViewModel vm) => vm.MyValue,
                converter: new IsStringNullOrWhiteSpaceConverter());
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IsStringNullOrWhiteSpaceConverterPage.xaml).

## API

You can find the source code for `IsStringNullOrWhiteSpaceConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IsStringNullOrWhiteSpaceConverter.shared.cs).
