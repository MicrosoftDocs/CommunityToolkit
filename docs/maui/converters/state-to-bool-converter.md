---
title: StateToBooleanConverter - .NET MAUI Community Toolkit
author: bijington
description: "The StateToBooleanConverter is a one way converter that returns a boolean result based on whether the supplied value is of a specific LayoutState."
ms.date: 05/17/2022
---

# StateToBooleanConverter

The `StateToBooleanConverter` is a one way converter that returns a `boolean` result based on whether the supplied value is of a specific `LayoutState`.

The `Convert` method returns a `boolean` result based on whether the supplied value is of a specific `LayoutState`. The `LayoutState` enum is provided by the toolkit and offers the possible values:

- `None`
- `Loading`
- `Saving`
- `Success`
- `Error`
- `Empty`
- `Custom`

> [!NOTE]
> Note that the expected `LayoutState` can be supplied in the following order of precedence:
> 1. as the `ConverterParameter` in the converter binding; this supersedes the `StateToCompare` property
> 2. as the `StateToCompare` property on the converter

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

The following example shows how to use the converter to change the visibility of a `Label` control based on the `LayoutState` property which is modified on a `Button` `Command`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the StateToBooleanConverter

The `StateToBooleanConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.StateToBooleanConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:StateToBooleanConverter x:Key="StateToBooleanConverter" StateToCompare="Success" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout VerticalOptions="Center">
        <Label
            HorizontalOptions="Center"
            IsVisible="{Binding LayoutState, Converter={StaticResource StateToBooleanConverter}}"
            Text="The state is Success!"
            VerticalOptions="Center" />
        <Button Command="{Binding ChangeLayoutCommand}" Text="Change state" />
    </VerticalStackLayout>

</ContentPage>
```

### C#

The `StateToBooleanConverter` can be used as follows in C#:

```csharp
class StateToBooleanConverterPage : ContentPage
{
    public StateToBooleanConverterPage()
    {
        var label = new Label
        {
            HorizontalOptions = LayoutOptions.Center,
            Text = "The state is Success!",
            VerticalOptions = LayoutOptions.Center
        };

        label.SetBinding(
            Label.IsVisibleProperty,
            new Binding(
                nameof(ViewModel.LayoutState),
                converter: new StateToBooleanConverter { StateToCompare = LayoutState.Success }));

        var button = new Button
        {
            Text = "Change state"
        };
    
        button.SetBinding(
            Button.CommandProperty,
            nameof(ViewModel.ChangeLayoutCommand));

        Content = new VerticalStackLayout
        {
            Children = 
            {
                label,
                button
            }
        };
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class StateToBooleanConverterPage : ContentPage
{
    public StateToBooleanConverterPage()
    {
        Content = new VerticalStackLayout
        {
            Children = 
            {
                new Label()
                    .Text("The state is Success!")
                    .CenterHorizontal()
                    .CenterVertical()
                    .Bind(
                        Label.IsVisibleProperty,
                        static (ViewModel vm) => vm.LayoutState,
                        converter: new StateToBooleanConverter { StateToCompare = LayoutState.Success }),

                new Button()
                    .Text("Change state")
                    .BindCommand(static (ViewModel vm) => vm.ChangeLayoutCommand)
            }
        };
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/StateToBooleanConverterPage.xaml).

## API

You can find the source code for `StateToBooleanConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/StateToBooleanConverter.shared.cs).
