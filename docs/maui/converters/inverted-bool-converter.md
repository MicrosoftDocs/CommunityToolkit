---
title: InvertedBoolConverter - .NET MAUI Community Toolkit
author: bijington
description: "The InvertedBoolConverter is a converter that allows users to convert a bool to its inverse - true becomes false and vice-versa."
ms.date: 03/16/2022
---

# InvertedBoolConverter

The `InvertedBoolConverter` is a converter that allows users to convert a `bool` to its inverse - `true` becomes `false` and vice-versa.

The `Convert` method returns `false` if the supplied `value` is equal to `true` and `true` otherwise.

The `ConvertBack` method returns `false` if the supplied `value` is `true` and `true` otherwise.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the InvertedBoolConverter

The `InvertedBoolConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.InvertedBoolConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:InvertedBoolConverter x:Key="InvertedBoolConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="The value is false."
           IsVisible="{Binding MyValue, Converter={StaticResource InvertedBoolConverter}}" />

</ContentPage>
```

### C#

The `InvertedBoolConverter` can be used as follows in C#:

```csharp
class InvertedBoolConverterPage : ContentPage
{
    public InvertedBoolConverterPage()
    {
        var label = new Label { Text = "The value is false." };

		label.SetBinding(
			Label.IsVisibleProperty,
			new Binding(
				nameof(ViewModels.MyValue),
				converter: new InvertedBoolConverter()));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class InvertedBoolConverterPage : ContentPage
{
    public InvertedBoolConverterPage()
    {
        Content = new Label { Text = "The value is false." }
            .Bind(
                Label.IsVisibleProperty,
                static (ViewModel vm) => vm.MyValue,
                converter: new InvertedBoolConverter());
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/InvertedBoolConverterPage.xaml).

## API

You can find the source code for `InvertedBoolConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/InvertedBoolConverter.shared.cs).
