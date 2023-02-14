---
title: IndexToArrayItemConverter - .NET MAUI Community Toolkit
author: cliffagius
description: "The IndexToArrayItemConverter is a converter that allows users to convert a int value binding to an item in an array. The int value being data bound represents the indexer used to access the array. The array is passed in through the ConverterParameter."
ms.date: 04/14/2022
---

# IndexToArrayItemConverter

The `IndexToArrayItemConverter` is a converter that allows users to convert an `int` value binding to an item in an array. The `int` value being data bound represents the indexer used to access the array. The array is passed in through the `ConverterParameter`.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the IndexToArrayItemConverter

The `IndexToArrayItemConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyLittleApp.MainPage">
    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:IndexToArrayItemConverter x:Key="IndexToArrayItemConverter" />
            <x:Array x:Key="MyArray" Type="x:String">
                <x:String>Value 1</x:String>
                <x:String>Value 2</x:String>
                <x:String>Value 3</x:String>
                <x:String>Value 4</x:String>
                <x:String>Value 5</x:String>
            </x:Array>
        </ResourceDictionary>
    </ContentPage.Resources>

    <StackLayout>

        <Label Text="{Binding MyIntegerValue, Converter={StaticResource IndexToArrayItemConverter}, ConverterParameter={StaticResource MyArray}}" />

    </StackLayout>
</ContentPage>
```

### C#

The `IndexToArrayItemConverter` can be used as follows in C#:

```csharp
class IndexToArrayItemConverter : ContentPage
{
    public IndexToArrayItemConverter()
    {
        var array = new string[] { "Value 1", "Value 2", "Value 3", "Value 4", "Value 5" };

        var label = new Label();

        label.SetBinding(
            Label.TextProperty, 
            new Binding(
                nameof(ViewModel.MyIntegerValue), 
                converter: new IndexToArrayItemConverter(), 
                converterParameter: array)); 

        Content = label;        
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class IndexToArrayItemConverter : ContentPage
{
    public IndexToArrayItemConverter()
    {
         var array = new string[] { "Value 1", "Value 2", "Value 3", "Value 4", "Value 5" };

        Content = new Label()
            .Bind(
                Label.TextProperty, 
                static (ViewModel vm) => vm.MyIntegerValue,
                converter: new IndexToArrayItemConverter(),
                converterParameter: array); 
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IndexToArrayItemConverterPage.xaml).

## API

You can find the source code for `IndexToArrayItemConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IndexToArrayItemConverter.shared.cs).
