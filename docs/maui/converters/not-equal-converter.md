---
title: .NET MAUI NotEqualConverter
author: bijington
description: "The NotEqualConverter is a one way converter that returns a `bool` indicating whether the binding value is not equal to another specified value."
ms.date: 03/02/2022
---

# NotEqualConverter

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `NotEqualConverter` is a one way converter that returns a `bool` indicating whether the binding value is not equal to another specified value.

The `Convert` method returns `true` when the binding `value` is **not equal** to the supplied `ConverterParameter`.

The `ConvertBack` method is not supported. For the opposite behavior see the [`EqualConverter`](equal-converter.md).

## Syntax

### XAML

The `NotEqualConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:mct="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.NotEqualConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <mct:NotEqualConverter x:Key="NotEqualConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="The value is not equal to 100"
           IsVisible="{Binding MyValue, Converter={StaticResource NotEqualConverter}, ConverterParameter=100}" />

</ContentPage>
```

### C#

The `NotEqualConverter` can be used as follows in C#:

```csharp

class NotEqualConverterPage : ContentPage
{
    public NotEqualConverterPage()
    {
        var label = new Label { Text = "The value is not equal to 100" };

		label.SetBinding(
			Label.IsVisibleProperty,
			new Binding(nameof(ViewModels.MyValue), converter: new NotEqualConverter());

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class NotEqualConverterPage : ContentPage
{
    public NotEqualConverterPage()
    {
        Content = new Label { Text = "The value is not equal to 100" }
            .Bind(Label.IsVisible, nameof(ViewModel.MyValue), converter: new NotEqualConverter();
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/NotEqualConverterPage.xaml).

## API

You can find the source code for `NotEqualConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/NotEqualConverter.cs).