---
title: BoolToObjectConverter - .NET MAUI Community Toolkit
author: bijington
description: "The BoolToObjectConverter is a converter that allows users to convert a bool value binding to a specific object."
ms.date: 04/15/2022
---

# BoolToObjectConverter

The `BoolToObjectConverter` is a converter that allows users to convert a `bool` value binding to a specific object. By providing both a TrueObject and a FalseObject in the converter the appropriate object will be returned depending on the value of the binding.

The `Convert` method returns the `TrueObject` if the supplied `value` is `true` or the `FalseObject` otherwise.

The `ConvertBack` method returns `true` if the supplied `value` is equal to the `TrueObject` or `false` otherwise.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following examples will show how to use the `BoolToObjectConverter` to change the visibility of a `Label` control based on the specific value of a bound property `MyValue`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the BoolToObjectConverter

The `BoolToObjectConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.BoolToObjectConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:BoolToObjectConverter x:Key="BoolToObjectConverter" TrueObject="42" FalseObject="0" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="The answer to the Ultimate Question of Life, the Universe and Everything."
           IsVisible="{Binding MyValue, Converter={StaticResource BoolToObjectConverter}}" />

</ContentPage>
```

### C#

The `BoolToObjectConverter` can be used as follows in C#:

```csharp
class BoolToObjectConverterPage : ContentPage
{
    public BoolToObjectConverterPage()
    {
        var label = new Label
        {
            Text = "The answer to the Ultimate Question of Life, the Universe and Everything."
        };

		label.SetBinding(
			Label.IsVisibleProperty,
			new Binding(
				nameof(ViewModels.MyValue),
				converter: new BoolToObjectConverter { TrueObject = 42, FalseObject = 0 }));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class BoolToObjectConverterPage : ContentPage
{
    public BoolToObjectConverterPage()
    {
        Content = new Label()
            .Text("The answer to the Ultimate Question of Life, the Universe and Everything.")
            .Bind(
                Label.IsVisibleProperty,
                static (ViewModel vm) => vm.MyValue,
                converter: new BoolToObjectConverter { TrueObject = 42, FalseObject = 0 });
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/BoolToObjectConverterPage.xaml).

## API

You can find the source code for `BoolToObjectConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/BoolToObjectConverter.shared.cs).
