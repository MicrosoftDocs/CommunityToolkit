---
title: ListToStringConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ListToStringConverter is a one way converter that returns a concatenation of the members of a collection, using the specified separator between each member."
ms.date: 03/30/2022
---

# ListToStringConverter

The `ListToStringConverter` is a one way converter that returns a concatenation of the members of a collection, using the specified separator between each member.

The `Convert` method returns a concatenation of the members of a collection, using the specified separator between each member.

> [!NOTE]
> Note that the separators can be supplied in the following ways:
> 1. As the `ConverterParameter` in the converter binding
> 2. As the `Separator` property on the converter
> 
> Note that the `ConverterParameter` option will take precedence over the `Separator` property.

The `ConvertBack` method is not supported. For the opposite behavior see the [`StringToListConverter`](string-to-list-converter.md).

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ListToStringConverter

The `ListToStringConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ListToStringConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ListToStringConverter x:Key="ListToStringConverter" Separator="," />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="{Binding MyListValue, Converter={StaticResource ListToStringConverter}}" />

</ContentPage>
```

### C#

The `ListToStringConverter` can be used as follows in C#:

```csharp
class ListToStringConverterPage : ContentPage
{
    public ListToStringConverterPage()
    {
        var label = new Label();

		label.SetBinding(
			Label.TextProperty,
			new Binding(
				nameof(ViewModels.MyListValue),
				converter: new ListToStringConverter() { Separator = "," }));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class ListToStringConverterPage : ContentPage
{
    public ListToStringConverterPage()
    {
        Content = new Label()
            .Bind(
                Label.TextProperty,
                static (ViewModel vm) => vm.MyListValue,
                converter: new ListToStringConverter(),
                converterParameter: ",");
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| Separator | `string` | The value that separates each item in the collection. This value is superseded by the ConverterParameter, if provided. If ConverterParameter is null, this Separator property will be used. |

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ListToStringConverterPage.xaml).

## API

You can find the source code for `ListToStringConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ListToStringConverter.shared.cs).
