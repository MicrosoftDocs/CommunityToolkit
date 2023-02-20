---
title: StatusBarBehavior - .NET MAUI Community Toolkit
author: pictos
description: "The StatusBarBehavior is a behavior allows you to control the statusbar's style."
ms.date: 09/27/2022
---

# StatusBarBehavior

The `StatusBarBehavior` allows you to customize the color and style of yours device statusbar.

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the StatusBarBehavior

The `StatusBarBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyLittleApp.MainPage">
    
    <ContentPage.Behaviors>
        <toolkit:StatusBarBehavior StatusBarColor="Fuchsia" StatusBarStyle="LightContent" />
    </ContentPage.Behaviors>

</ContentPage>
```

### C#

The `StatusBarBehavior` can be used as follows in C#:

```csharp
class MyPage : ContentPage
{
    public MyPage()
    {
        this.Behaviors.Add(new StatusBarBehavior
        {
            StatusBarColor = Colors.Red,
            StatusBarStyle = StatusBarStyle.LightContent
        });
    }
}
```

There's another way to access the Statusbar APIs on C#, you can call the methods directly, as you can see in the snippet below:

```csharp
class MyPage : ContentPage
{
    protected override void OnNavigatedTo(NavigatedToEventArgs args)
    {
        base.OnNavigatedTo(args);
        CommunityToolkit.Maui.Core.Platform.StatusBar.SetColor(statusBarColor);
        CommunityToolkit.Maui.Core.Platform.StatusBar.SetStyle(StatusBarStyle.LightContent);
    }
}
```

> [!WARNING]
> If you want to add this code the `MainPage`'s constructor, `OnAppearing` or `OnNavigatedTo` methods, please use the `Behavior` instead.
> Using directly on these places can crash your application since the platform-specific components may not be initialized.

## Configuration

# [Android](#tab/android)

No changes needed.

# [iOS](#tab/ios)

In the _Platforms/iOS/Info.plist_ file, add the following key and value:

```xml
    <key>UIViewControllerBasedStatusBarAppearance</key>
    <false/>
```

-----

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| StatusBarColor | Color | The `Color` name from the Microsoft.Maui.Graphics namespace. |
| StatusBarStyle | StatusBarStyle | The style used by statusbar, can be LightContent, DarkContent or Default. |

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/StatusBarBehaviorPage.xaml).

## API

You can find the source code for `StatusBarBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/PlatformBehaviors/StatusBar/StatusBarBehavior.shared.cs).
