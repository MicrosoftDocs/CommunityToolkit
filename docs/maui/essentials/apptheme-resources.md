---
title: AppTheme Resources - .NET MAUI Community Toolkit
author: jfversluis
description: With AppThemeResource and AppThemeColor you can create theme aware resources for your application that automatically update when the device theme updates.
ms.date: 07/13/2023
---

# AppTheme Resources

With `AppThemeResource` and `AppThemeColor` you can create theme-aware resources for your application that automatically update when the device theme updates.

The `AppThemeResource` and `AppThemeColor` objects are theme-aware resources that will make it easier to work with colors, images, and other resources that need to change depending on the app's current theme.
These objects build upon the concepts of the [`AppThemeBinding`](/dotnet/maui/user-interface/system-theme-changes) that is available in .NET MAUI, and will make it easier to work with these types of resources in a [`ResourceDictionary`](/dotnet/maui/fundamentals/resource-dictionaries).

Because of this, you should typically use these APIs through the `ThemeResource` markup extension in XAML.

## Syntax

### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### AppThemeResource

The `AppThemeResource` is a generic theme-aware object that allows you to set any `object` for the `Light`, `Dark` and `Default` properties. Because `AppThemeResource` is not strongly-typed, at runtime the values for each property will be evaluated and casted.

> [!WARNING]
>
> If the cast is invalid, this might result in a runtime exception.

The following example shows how to use `AppThemeResource` through a `ResourceDictionary`:

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.MyPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    <ContentPage.Resources>
        <toolkit:AppThemeResource Light="dark.png" Dark="light.png" x:Key="MyImageSource" />
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Image Source="{toolkit:ThemeResource ImageSource}" />
    </VerticalStackLayout>
</ContentPage>
```

#### AppThemeColor

The `AppThemeColor` is a specialized theme-aware [`Color`](xref:Microsoft.Maui.Graphics.Color) that allows you to set a `Color` for the `Light`, `Dark` and `Default` properties.

The following example shows how to use `AppThemeColor` through a `ResourceDictionary`:

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.MyPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    <ContentPage.Resources>
        <toolkit:AppThemeColor Light="Red" Dark="Green" x:Key="LabelTextColor" />
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Label TextColor="{toolkit:ThemeResource LabelTextColor}" />
    </VerticalStackLayout>
</ContentPage>
```

#### Consuming AppThemeColor and AppThemeResource Through Styles

Because we can use these theme-aware resources in a `ResourceDictionary`, that means we can also consume them through a `Style`.

The following example shows how to use `AppThemeColor` through a `Style`:

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.MyPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    <ContentPage.Resources>
        <toolkit:AppThemeColor Light="Red" Dark="Green" x:Key="LabelTextColor" />

        <Style x:Key="Headline" TargetType="Label">
            <Setter Property="FontFamily" Value="Segoe UI" />
            <Setter Property="FontSize" Value="10" />
            <Setter Property="TextColor" Value="{toolkit:ThemeResource LabelTextColor}" />
        </Style>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Label Style="{StaticResource Headline}" />
    </VerticalStackLayout>
</ContentPage>
```

## Extensibility

Both `AppThemeResource` and `AppThemeColor` inherit from the abstract class `AppThemeObject<T>`. If you have a need for a more strongly typed resource that is not available in the .NET MAUI Community Toolkit, you can create your own inheritance.

## Properties

THe below table describes the properties for `AppThemeResource` and `AppThemeColor`. For `AppThemeColor`, the types of each property will be `Color` instead of `object`.

| Property | Type | Description |
|---|---|---|
| Dark | `object` | The value that is applied to the property that this resource is applied to when the app uses the dark theme. |
| Default | `object` | The value that is applied to the property that this resource is applied to when the app uses the light or dark theme and there is no value provided for the corresponding property of that theme. |
| Light | `object` | The  value that is applied to the property that this resource is applied to when the app uses the light theme. |

## Examples

You can find an example of `AppThemeResource` in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Essentials/AppThemePage.xaml).

## API

You can find the source code for `AppThemeResource` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Essentials/AppTheme/AppThemeObjectOfT.shared.cs).
