---
title: IsListNotNullOrEmptyConverter - .NET MAUI Community Toolkit
author: bijington
description: "The IsListNotNullOrEmptyConverter is a one way converter that converts IEnumerable to a bool value."
ms.date: 02/11/2022
---

# IsListNotNullOrEmptyConverter

The `IsListNotNullOrEmptyConverter` is a one way converter that converts `IEnumerable` to a `bool` value. 

The `Convert` method returns `false` when `null` or an empty `IEnumerable` is passed in or `true` otherwise.

The `ConvertBack` method is not supported. For the opposite behavior see the [`IsListNullOrEmptyConverter`](is-list-null-or-empty-converter.md).

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the IsListNotNullOrEmptyConverter

The `IsListNotNullOrEmptyConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.IsListNotNullOrEmptyConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:IsListNotNullOrEmptyConverter x:Key="IsListNotNullOrEmptyConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="The list is not empty"
           IsVisible="{Binding MyList, Converter={StaticResource IsListNotNullOrEmptyConverter}}" />

</ContentPage>
```

### C#

The `IsListNotNullOrEmptyConverter` can be used as follows in C#:

```csharp

class IsListNotNullOrEmptyConverterPage : ContentPage
{
    public IsListNotNullOrEmptyConverterPage()
    {
        var label = new Label { Text = "The list is not empty" };

		label.SetBinding(
			Label.IsVisibleProperty,
			new Binding(nameof(ViewModels.MyList), converter: new IsListNotNullOrEmptyConverter()));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class IsListNotNullOrEmptyConverterPage : ContentPage
{
    public IsListNotNullOrEmptyConverterPage()
    {
        Content = new Label { Text = "The list is not empty" }
            .Bind(
                Label.IsVisibleProperty,
                static (ViewModel vm) => vm.MyList,
                converter: new IsListNotNullOrEmptyConverter());
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IsListNotNullOrEmptyConverterPage.xaml).

## API

You can find the source code for `IsListNotNullOrEmptyConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IsListNotNullOrEmptyConverter.shared.cs).
