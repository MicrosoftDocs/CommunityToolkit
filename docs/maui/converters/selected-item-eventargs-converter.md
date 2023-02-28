---
title: SelectedItemEventArgsConverter - .NET MAUI Community Toolkit
author: cliffagius
description: "The SelectedItemEventArgsConverter is a converter that allows users to extract the SelectedItem value from an SelectedItemChangedEventArgs object. It can subsequently be used in combination with EventToCommandBehavior"
ms.date: 04/23/2022
---

# SelectedItemEventArgsConverter

The `SelectedItemEventArgsConverter` is a converter that allows users to extract the SelectedItem value from an `SelectedItemChangedEventArgs` object. It can subsequently be used in combination with [EventToCommandBehavior](../behaviors/event-to-command-behavior.md).

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the SelectedItemEventArgsConverter

The `SelectedItemEventArgsConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyLittleApp.MainPage">
    <ContentPage.Resources>
         <ResourceDictionary>
             <toolkit:SelectedItemEventArgsConverter x:Key="SelectedItemEventArgsConverter" />
         </ResourceDictionary>
    </ContentPage.Resources>

     <VerticalStackLayout Padding="10">

        <Label
            Text="The SelectedItemEventArgsConverter is a converter that allows users to extract the SelectedItem value from an SelectedItemChangedEventArgs object. It can subsequently be used in combination with EventToCommandBehavior."
            TextColor="{StaticResource NormalLabelTextColor}"
            Margin="0, 0, 0, 20" />

        <ListView
            BackgroundColor="Transparent"
            ItemsSource="{Binding Items}"
            SelectedItem="{Binding ItemSelected, Mode=TwoWay}">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <ViewCell>
                        <VerticalStackLayout Margin="6">
                            <Label Text="{Binding Name, StringFormat='Name: {0}'}"/>
                        </VerticalStackLayout>
                    </ViewCell>
                </DataTemplate>
            </ListView.ItemTemplate>
            <ListView.Behaviors>
                <toolkit:EventToCommandBehavior EventName="ItemSelected"
                                                Command="{Binding ItemSelectedCommand}"
                                                EventArgsConverter="{StaticResource SelectedItemEventArgsConverter}" />
            </ListView.Behaviors>
        </ListView>
    </VerticalStackLayout>
</ContentPage>
```

### C#

The `SelectedItemEventArgsConverter` can be used as follows in C#:

```csharp
class SelectedItemEventArgsConverterPage : ContentPage
{
    public SelectedItemEventArgsConverterPage()
    {
        var behavior = new EventToCommandBehavior
        {
            EventName = nameof(ListView.ItemSelected),
            EventArgsConverter = new SelectedItemEventArgsConverter()
        };
        behavior.SetBinding(EventToCommandBehavior.CommandProperty, nameof(ViewModel.ItemSelectedCommand);

        var listView = new ListView 
        { 
            HasUnevenRows = true 
        };
        listView.SetBinding(ListView.ItemsSource, nameof(ViewModel.Items));
        listView.Behaviors.Add(behavior);

        Content = listView;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class SelectedItemEventArgsConverterPage : ContentPage
{
    public SelectedItemEventArgsConverterPage()
    {
        Content = new ListView
        {
            HasUnevenRows = true
        }
        .Bind(
            ListView.ItemsSourceProperty,
            static (ViewModel vm) => vm.Items)
        .Behaviors(
            new EventToCommandBehavior
            {
                EventName = nameof(ListView.ItemSelected),
                EventArgsConverter = new SelectedItemEventArgsConverter()
            }
            .Bind(
                EventToCommandBehavior.CommandProperty, 
                nameof(ViewModel.ItemTappedCommand)));                   
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/SelectedItemEventArgsConverterPage.xaml).

## API

You can find the source code for `SelectedItemEventArgsConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/SelectedItemEventArgsConverter.shared.cs).
