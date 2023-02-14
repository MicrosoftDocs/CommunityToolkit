---
title: IsInRangeConverter - .NET MAUI Community Toolkit
author: GeorgeLeithead
description: "The IsInRangeConverter is a one-way converter that takes an incoming value implementing IComparable, and a minimum and maximum value, and returns the result of the value being between the minimum and maximum values."
ms.date: 11/26/2022
---

# IsInRangeConverter

The `IsInRangeConverter` is a one-way converter that takes an incoming value implementing `IComparable`, and returns the result of the value being between the minimum and maximum values. The result will default to a `bool` if no objects were specified through the `TrueObject` and/or `FalseObject` properties. If values are assigned to the `TrueObject` and `FalseObject` properties, the IsInRangeConverter returns the respective object assigned.

> [!NOTE]
> Note that the either **both** the `TrueObject` and `FalseObject` should have a value defined or **neither** should.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the IsInRangeConverter

The `IsInRangeConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.IsInRangeConverterPage">
        <ResourceDictionary>
            <x:String x:Key="MinValue">Hello</x:String>
            <x:String x:Key="MaxValue">World</x:String>
            <Color x:Key="TrueColor">Green</Color>
            <Color x:Key="FalseColor">Red</Color>
        </ResourceDictionary>

    <Label BackgroundColor="{Binding MyValue, Converter={toolkit:IsInRangeConverter TrueObject={StaticResource TrueColor}, FalseObject={StaticResource FalseColor}, MinValue={StaticResource MinValue}, MaxValue={StaticResource MaxValue}}}" Text="The background of this label will be green if MyValue is between 'Hello' and 'World', otherwise red." />

</ContentPage>
```

### C#

The `IsInRangeConverter` can be used as follows in C#:

```csharp

class IsInRangeConverterPage : ContentPage
{
    public IsInRangeConverterPage()
    {
        Content = new Label()
            .Text("The background of this label will be green if MyValue is between 'Hello' and 'World', otherwise red.")
            .Bind(
                Label.BackgroundColorProperty,
                static (ViewModel vm) => vm.MyValue,
                converter: new IsInRangeConverter
                {
                        TrueObject = Colors.Green,
                        FalseObject = Colors.Red,
                        MinValue = "Hello",
                        MaxValue = "World"
                });
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| MinValue | `IComparable` | The minimum value for the compare range. |
| MaxValue | `IComparable` | The maximum value for the compare range. |
| FalseObject | `object` | The result to return if the comparison results in a `false` comparison. |
| TrueObject | `object` | The result to return if the comparison results in a `true` comparison. |

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IsInRangeConverterPage.cs).

## API

You can find the source code for `IsInRangeConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IsInRangeConverter.shared.cs).