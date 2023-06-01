---
title: LazyView - .NET MAUI Community Toolkit
author: kphillpotts
description: The LazyView control allows you to delay the initialization of a View.
ms.date: 03/29/2023
---

# LazyView

The `LazyView` control allows you to delay the initialization of a `View`. You need to provide the type of the `View` that you want to be rendered, using the `x:TypeArguments` XAML namespace attribute, and handle its initialization using the `LoadViewAsync` method. The `HasLazyViewLoaded` property can be examined to determine when the `LazyView` is loaded.

## Syntax

### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

### Using the LazyView

```xaml
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
    x:Class="CommunityToolkit.Maui.Sample.Pages.Views.LazyViewPage"
    xmlns:local="clr-namespace:CommunityToolkit.Maui.Sample.Pages.Views.LazyView"
    Title="Lazy View">

    <StackLayout>
        <toolkit:LazyView x:Name="LazyUserAction" x:TypeArguments="local:LazyTestView" />
        <Button Text="Load View Now" Clicked="LoadLazyView_Clicked" />
    </StackLayout>

</ContentPage>
```

In your code behind, you can make the view load by calling the `LoadViewAsync` method.

```csharp
async void LoadLazyView_Clicked(object sender, EventArgs e)
{
    await LazyUserAction.LoadViewAsync();
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| HasLazyViewLoaded | bool| Gets the loaded status of the `LazyView`. |


## Methods

|Property  |Return Type  |Description  |
|---------|---------|---------|
| LoadViewAsync | ValueTask| Initialize the `View`. |

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/LazyView/).

## API

You can find the source code for `LazyView` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/tree/main/src/CommunityToolkit.Maui/Views/LazyView).
