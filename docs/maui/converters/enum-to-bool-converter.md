---
title: EnumToBoolConverter - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The EnumToBoolConverter is a one way converter that allows you to convert an Enum to a corresponding bool based on whether it is equal to a set of supplied enum values."
ms.date: 05/04/2022
---

# EnumToBoolConverter

The `EnumToBoolConverter` is a on way converter that allows you to convert an `Enum` to a corresponding `bool` based on whether it is equal to a set of supplied enum values. It is useful when binding a collection of values representing an enumeration type to a boolean control property like the `IsVisible` property.

The `Convert` method returns the supplied `value` converted to an `bool` based on whether the `value` is equal to any of the defined `TrueValues` or the supplied `CommandParameter`.

The `ConvertBack` method is not supported.

> [!NOTE]
> Note that the 'true' value to compare to can be supplied in the following ways:
> 1. as the `TrueValue` property on the converter.
> 1. as the `ConverterParameter` in the converter binding,
> 
> Note that the `TrueValues` property will take precedence over the `ConverterParameter` option.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

Each of the following examples make use of the following enum definition:

```csharp
namespace MyLittleApp;

public enum MyDevicePlatform
{
    Android,
    iOS,
    macOS,
    Tizen,
    Windows
}
```

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the EnumToBoolConverter

The `EnumToBoolConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             xmlns:mylittleapp="clr-namespace:MyLittleApp"
             x:Class="MyLittleApp.MainPage">
    <ContentPage.Resources>
         <ResourceDictionary>
             <toolkit:EnumToBoolConverter x:Key="MobileConverter">
                <toolkit:EnumToBoolConverter.TrueValues>
                    <mylittleapp:MyDevicePlatform>Android</mylittleapp:MyDevicePlatform>
                    <mylittleapp:MyDevicePlatform>iOS</mylittleapp:MyDevicePlatform>
                </toolkit:EnumToBoolConverter.TrueValues>
            </toolkit:EnumToBoolConverter>
         </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Picker ItemsSource="{Binding Platforms}"
                SelectedItem="{Binding SelectedPlatform}" />
        <Label IsVisible="{Binding SelectedPlatform, Converter={StaticResource MobileConverter}}"
               Text="I am visible when the Picker value is Android or iOS."/>
    </VerticalStackLayout>
</ContentPage>
```

It is also possible to pass the converter parameter:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyLittleApp.MainPage">
    <ContentPage.Resources>
         <ResourceDictionary>
             <toolkit:EnumToBoolConverter x:Key="PlatformConverter" />
         </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Picker ItemsSource="{Binding Platforms}"
                SelectedItem="{Binding SelectedPlatform}" />
        <Label IsVisible="{Binding SelectedPlatform, Converter={StaticResource PlatformConverter}, ConverterParameter={x:Static vm:MyDevicePlatform.Tizen}}"
               Text="I am visible when the Picker value is Tizen."/>
    </VerticalStackLayout>
</ContentPage>
```

### C#

The `EnumToBoolConverter` can be used as follows in C#:

```csharp
class EnumToBoolConverterPage : ContentPage
{
    public EnumToBoolConverterPage()
    {
        var picker = new Picker();
        picker.SetBinding(Picker.ItemsSourceProperty, nameof(ViewModel.Platforms));
        picker.SetBinding(Picker.SelectedItemProperty, nameof(ViewModel.SelectedPlatform));

        var label = new Label
        {
            Text = "I am visible when the Picker value is Tizen."
        };

		label.SetBinding(
			Label.IsVisibleProperty,
			new Binding(
				nameof(ViewModel.SelectedPlatform),
				converter: new EnumToBoolConverter(),
                converterParameter: MyDevicePlatform.Tizen));

		Content = new VerticalStackLayout
        {
            Children = { picker, label }
        };
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class EnumToBoolConverterPage : ContentPage
{
    public EnumToBoolConverterPage()
    {
        Content = new VerticalStackLayout
        {
            Children = 
            {
                new Picker()
                    .Bind(
                        Picker.ItemsSourceProperty, 
                        static (ViewModel vm) => vm.Platforms)
                    .Bind(
                        Picker.SelectedItemProperty,
                        static (ViewModel vm) => vm.SelectedPlatform),

                new Label()
                    .Text("I am visible when the Picker value is Tizen.")
                    .Bind(
                        Label.IsVisibleProperty,
                        static (ViewModel vm) => vm.SelectedPlatform,
                        converter: new EnumToBoolConverter(),
                        converterParameter: MyDevicePlatform.Tizen)
            }
        };
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| TrueValues | `IList<Enum>` | Enum values, that converts to `true` (optional).  |


## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/EnumToBoolConverterPage.xaml).

## API

You can find the source code for `EnumToBoolConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/EnumToBoolConverter.shared.cs).
