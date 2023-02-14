---
title: IsNullConverter - .NET MAUI Community Toolkit
author: IeuanWalker
description: "The IsNullConverter is a converter that allows users to convert an incoming binding to a bool value. This value represents if the incoming binding value is null."
ms.date: 04/18/2022
---

# IsNullConverter

The `IsNullConverter` is a one way converter that converts `Object?` to a `bool` value. 

The `Convert` method returns `true` when the binded object is `null` or `false` otherwise.

The `ConvertBack` method is not supported. For the opposite behavior see the [`IsNotNullConverter`](is-not-null-converter.md).

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the IsNullConverter

The `IsNullConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.IsNullConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:IsNullConverter x:Key="IsNullConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="Object is null"
           IsVisible="{Binding MyObject, Converter={StaticResource IsNullConverter}}" />

</ContentPage>
```

### C#

The `IsNullConverter` can be used as follows in C#:

```csharp

class IsNullConverterPage : ContentPage
{
    public IsNullConverterPage()
    {
        var label = new Label { Text = "Object is null" };

        label.SetBinding(
                Label.IsVisibleProperty,
                new Binding(nameof(ViewModels.MyObject), converter: new IsNullConverter()));

        Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class IsNullConverterPage : ContentPage
{
    public IsNullConverterPage()
    {
        Content = new Label { Text = "Object is null" }
            .Bind(Label.IsVisibleProperty, nameof(ViewModel.MyObject), converter: new IsNullConverter());
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IsNullConverterPage.xaml).

## API

You can find the source code for `IsNullConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IsNullConverter.shared.cs).
