---
title: CompareConverter - .NET MAUI Community Toolkit
author: bijington
description: "The CompareConverter is a one way converter that takes an incoming value implementing IComparable, compares to a specified value, and returns the comparison result."
ms.date: 05/17/2022
---

# CompareConverter

The `CompareConverter` is a one way converter that takes an incoming value implementing `IComparable`, compares to a specified value, and returns the comparison result. The result will default to a `bool` if no objects were specified through the `TrueObject` and/or `FalseObject` properties. If values are assigned to the `TrueObject` and/or `FalseObject` properties, the CompareConverter returns the respective object assigned.

> [!NOTE]
> Note that the either **both** the `TrueObject` and `FalseObject` should have a value defined or **neither** should.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the CompareConverter

The `CompareConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.CompareConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <x:Int32 x:Key="Threshold">50</x:Int32>
            <Color x:Key="EqualOrGreaterThanThresholdColor">LightGreen</Color>
            <Color x:Key="SmallerThanThresholdColor">PaleVioletRed</Color>

            <toolkit:CompareConverter
                x:Key="CompareConverter"
                ComparisonOperator="Smaller"
                ComparingValue="{StaticResource Threshold}"
                TrueObject="{StaticResource EqualOrGreaterThanThresholdColor}"
                FalseObject="{StaticResource SmallerThanThresholdColor}" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label
        Text="The background of this label will be green if the value entered is less than 50, and red otherwise." 
        BackgroundColor="{Binding MyValue, Converter={StaticResource CompareConverter}" />

</ContentPage>
```

> [!NOTE]
> In order to provide more concise XAML when using the converter it is recommended to create a sub-class of the `CompareConverter`. The following example shows how this can be achieved based on the original example.

#### Creating a CompareConverter

The following example shows how to create your own `CompareConverter` implementation that will compare `double` values and return a `Color` based on the result of the comparison.

```csharp
namespace CommunityToolkit.Maui.Sample.Converters;

public sealed class CompareDoubleToColorConverter : CompareConverter<double, Color>
{
}
```

It is then possible to use that converter in XAML as follows:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:converters="clr-namespace:CommunityToolkit.Maui.Sample.Converters"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.CompareConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:CompareConverter
                x:Key="CompareConverter"
                ComparisonOperator="Smaller"
                ComparingValue="50"
                TrueObject="LightGreen"
                FalseObject="PaleVioletRed" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label
        Text="The background of this label will be green if the value entered is less than 50, and red otherwise." 
        BackgroundColor="{Binding MyValue, Converter={StaticResource CompareConverter}" />

</ContentPage>
```

### C#

The `CompareConverter` can be used as follows in C#:

```csharp

class CompareConverterPage : ContentPage
{
    public CompareConverterPage()
    {
        var label = new Label
        {
            Text = "The background of this label will be green if the value entered is less than 50, and red otherwise."
        };

        label.SetBinding(
            Label.BackgroundColorProperty,
            new Binding(
                static (ViewModel vm) => vm.MyValue,
                converter: new CompareConverter
                {
                    ComparisonOperator = OperatorType.Smaller,
                    ComparingValue = 50,
                    TrueObject = Colors.LightGreen,
                    FalseObject = Colors.PaleVioletRed
                }));

        Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class CompareConverterPage : ContentPage
{
    public CompareConverterPage()
    {
        Content = new Label()
            .Text("The background of this label will be green if the value entered is less than 50, and red otherwise.")
            .Bind(
                Label.BackgroundColorProperty,
                static (ViewModel vm) => vm.MyValue,
                converter: new CompareConverter
                {
                    ComparisonOperator = OperatorType.Smaller,
                    ComparingValue = 50,
                    TrueObject = Colors.LightGreen,
                    FalseObject = Colors.PaleVioletRed
                });
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| ComparisonOperator | `OperatorType` | The type of casing to apply to the `string` value. |
| ComparingValue | `IComparable` | The value to compare against. |
| FalseObject | `object` | The result to return if the comparison results in a `false` comparison. |
| TrueObject | `object` | The result to return if the comparison results in a `true` comparison. |

### OperatorType

The `OperatorType` enumeration defines the following members:

- `NotEqual`
- `Smaller`
- `SmallerOrEqual`
- `Equal`
- `Greater`
- `GreaterOrEqual`

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/CompareConverterPage.xaml).

## API

You can find the source code for `CompareConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/CompareConverter.shared.cs).
