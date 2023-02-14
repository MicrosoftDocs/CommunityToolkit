---
title: IsNotNullConverter - .NET MAUI Community Toolkit
author: IeuanWalker
description: "The IsNotNullConverter is a converter that allows users to convert an incoming binding to a bool value. This value represents if the incoming binding value is not null."
ms.date: 04/18/2022
---

# IsNotNullConverter

The `IsNotNullConverter` is a one way converter that converts `Object?` to a `bool` value. 

The `Convert` method returns `false` when the binded object is `null` or `true` otherwise.

The `ConvertBack` method is not supported. For the opposite behavior see the [`IsNullConverter`](is-null-converter.md).

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the IsNotNullConverter

The `IsNotNullConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.IsNotNullConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:IsNotNullConverter x:Key="IsNotNullConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="Object is not null"
           IsVisible="{Binding MyObject, Converter={StaticResource IsNotNullConverter}}" />

</ContentPage>
```

### C#

The `IsNotNullConverter` can be used as follows in C#:

```csharp

class IsNotNullConverterPage : ContentPage
{
    public IsNotNullConverterPage()
    {
        var label = new Label { Text = "Object is not null" };

		label.SetBinding(
			Label.IsVisibleProperty,
			new Binding(nameof(ViewModels.MyObject), converter: new IsNotNullConverter()));

		Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class IsNotNullConverterPage : ContentPage
{
    public IsNotNullConverterPage()
    {
        Content = new Label { Text = "Object is not null" }
            .Bind(
                Label.IsVisibleProperty,
                static (ViewModel vm) => vm.MyObject,
                converter: new IsNotNullConverter());
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/IsNotNullConverterPage.xaml).

## API

You can find the source code for `IsNotNullConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/IsNotNullConverter.shared.cs).
