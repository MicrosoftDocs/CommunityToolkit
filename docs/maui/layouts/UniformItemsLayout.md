---
title: UniformItemsLayout - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: The UniformItemsLayout is a layout where all rows and columns have the same size.
ms.date: 04/12/2022
---

# UniformItemsLayout

The `UniformItemsLayout` is a layout where all rows and columns have the same size.

## Building an UniformItemsLayout

An `UniformItemsLayout` can be created in XAML or C#:

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the UniformItemsLayout

```xml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyProject.MyContentPage">

    <toolkit:UniformItemsLayout>
        <BoxView BackgroundColor="Blue" HeightRequest="25" WidthRequest="25"/>
        <BoxView BackgroundColor="Yellow" HeightRequest="25" WidthRequest="25"/>
        <BoxView BackgroundColor="Red" HeightRequest="25" WidthRequest="25"/>
        <BoxView BackgroundColor="Black" HeightRequest="25" WidthRequest="25"/>
    </toolkit:UniformItemsLayout>
    
</ContentPage>
```

### C#

```csharp
using CommunityToolkit.Maui.Views;

var page = new ContentPage
{
    Content = new UniformItemsLayout
    {
        Children = 
        {
            new BoxView { HeightRequest = 25, WidthRequest = 25, BackgroundColor = Colors.Blue },
            new BoxView { HeightRequest = 25, WidthRequest = 25, BackgroundColor = Colors.Yellow },
            new BoxView { HeightRequest = 25, WidthRequest = 25, BackgroundColor = Colors.Red },
            new BoxView { HeightRequest = 25, WidthRequest = 25, BackgroundColor = Colors.Black }
        }
    }
};
```

## Customizing an UniformItemsLayout

An `UniformItemsLayout` allows to limit the maximum number of columns and rows:

### XAML

```xml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyProject.MyContentPage">

    <toolkit:UniformItemsLayout MaxRows="1" MaxColumns="1">
        <BoxView BackgroundColor="Blue" HeightRequest="25" WidthRequest="25"/>
        <BoxView BackgroundColor="Yellow" HeightRequest="25" WidthRequest="25"/>
        <BoxView BackgroundColor="Red" HeightRequest="25" WidthRequest="25"/>
        <BoxView BackgroundColor="Black" HeightRequest="25" WidthRequest="25"/>
    </toolkit:UniformItemsLayout>
    
</ContentPage>
```

### C#

```csharp
using CommunityToolkit.Maui.Views;

var page = new ContentPage
{
    Content = new UniformItemsLayout
    {
        MaxRows = 1,
        MaxColumns = 1,
        Children = 
        {
            new BoxView { HeightRequest = 25, WidthRequest = 25, BackgroundColor = Colors.Blue },
            new BoxView { HeightRequest = 25, WidthRequest = 25, BackgroundColor = Colors.Yellow },
            new BoxView { HeightRequest = 25, WidthRequest = 25, BackgroundColor = Colors.Red },
            new BoxView { HeightRequest = 25, WidthRequest = 25, BackgroundColor = Colors.Black }
        }
    }
};
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| `MaxColumns  ` | `int` | Gets or sets the maximum number of items in a row. |
| `MaxRows ` | `int` | Gets or sets the maximum number of items in a column. |

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Layouts/).

## API

You can find the source code for `UniformItemsLayout` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/tree/main/src/CommunityToolkit.Maui/Layouts/UniformItemsLayout).
