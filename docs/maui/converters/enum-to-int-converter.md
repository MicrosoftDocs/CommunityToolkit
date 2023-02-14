---
title: EnumToIntConverter - .NET MAUI Community Toolkit
author: cliffagius
description: "The EnumToIntConverter is a converter that allows you to convert a standard Enum (extending int) to its underlying primitive int type."
ms.date: 04/12/2022
---

# EnumToIntConverter

The `EnumToIntConverter` is a converter that allows you to convert a standard `Enum` (extending int) to its underlying primitive `int` type. It is useful when binding a collection of values representing an enumeration type with default numbering to a control such as a `Picker`.

> [!NOTE]
> The `ConverterParameter` property is required and it should be set to the type of the enum to convert back to, when using a `TwoWay` or `OneWayToSource` binding. Otherwise an `ArgumentNullException` will be thrown. This is to allow for validating whether the `int` is a valid value in the enum.

For localization purposes or due to other requirements, the enum values often need to be converted to a human-readable string. In this case, when the user selects a value, the resulting `SelectedIndex` can easily be converted to the underlying `enum` value without requiring additional work in the associated ViewModel.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the EnumToIntConverter

The `EnumToIntConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyLittleApp.MainPage">
    <ContentPage.Resources>
         <ResourceDictionary>
             <toolkit:EnumToIntConverter x:Key="EnumToIntConverter" />
         </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout Padding="10,10" Spacing="10">
            <Label Text="The EnumToIntConverter is a converter that allows users to convert a standard enum (extending int) to its underlying primitive int type." 
                   TextColor="{StaticResource NormalLabelTextColor}" />
            <Label Text="Selecting a value from the picker will change the enum property in the view model" 
                   TextColor="{StaticResource NormalLabelTextColor}" />
            <Picker ItemsSource="{Binding AllStates}" 
                    SelectedIndex="{Binding SelectedState, Converter={StaticResource EnumToIntConverter}}" 
                    TextColor="{StaticResource NormalLabelTextColor}" />
            <Label Text="This label binds to the SelectedIndex property of the picker, both use EnumToIntConverter, so no int properties are necessary in ViewModel"
                   TextColor="{StaticResource NormalLabelTextColor}" />
            <Label Text="{Binding Path=SelectedState, Converter={StaticResource EnumToIntConverter}}" 
                   TextColor="{StaticResource NormalLabelTextColor}" />
        </VerticalStackLayout>
</ContentPage>
```

### C#

The `EnumToIntConverter` can be used as follows in C#:

```csharp
class EnumToIntConverterPage : ContentPage
{
    public EnumToIntConverterPage()
    {
      Picker picker = new Picker { Title = "EnumToIntConverter" };
      picker.SetBinding(Picker.ItemsSourceProperty, nameof(ViewModel.AllStates));
      picker.SetBinding(Picker.SelectedItemProperty, nameof(ViewModel.SelectedState));

      Content = new StackLayout
			{
				Margin = new Thickness(20),
				Children = {
					new Label {
						Text = "The EnumToIntConverter is a converter that allows users to convert a standard enum (extending int) to its underlying primitive int type.",
						FontAttributes = FontAttributes.Bold,
						HorizontalOptions = LayoutOptions.Center 
					},
					picker
				}
			};
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class EnumToIntConverterPage : ContentPage
{
    public EnumToIntConverterPage()
    {
        Content = new StackLayout {
          new Picker()
            .Bind(
                Picker.ItemSourceProperty,
                static (ViewModel vm) => vm.AllStates)
            .Bind(
                Picker.SelectedIndexProperty,
                static (ViewModel vm) => vm.SelectedState),

          new Label()
            .Bind(
                Label.TextProperty,
                static (ViewModel vm) => vm.SelectedState,
                converter: new EnumToIntConverter()),
        }
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/EnumToIntConverterPage.xaml).

## API

You can find the source code for `EnumToIntConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/EnumToIntConverter.shared.cs).
