---
title: StatusBarBehavior - .NET MAUI Community Toolkit
author: pictos
description: "The StatusBarBehavior provides the ability to customize the color and style of a devices status bar."
ms.date: 09/27/2022
---

# StatusBarBehavior

The `StatusBarBehavior` provides the ability to customize the color and style of a devices status bar.

The `StatusBarBehavior` applies the color and style values when the properties are updated. The values are also applied based on the `ApplyOn` property, this property makes it possible to define which lifecycle event is used:

- `StatusBarApplyOn.OnBehaviorAttachedTo` - Applies the color and style when the behavior has been attached to a page. **This is the default.**
- `StatusBarApplyOn.OnPageNavigatedTo` - Applies the color and style when the page has been navigated to.

> [!NOTE]
> If your application changes the status bar appearance on a per page basis then you should make use of the `StatusBarApplyOn.OnPageNavigatedTo` value for the `ApplyOn` property. Otherwise when navigating back the system will preserve the status bar appearance from the page the user navigated from and not to.

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
| ApplyOn | StatusBarBehavior | When to apply the status bar color and style. |
| StatusBarColor | Color | The `Color` name from the Microsoft.Maui.Graphics namespace. |
| StatusBarStyle | StatusBarStyle | The style used by statusbar, can be LightContent, DarkContent or Default. |

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/StatusBarBehaviorPage.xaml).

## API

You can find the source code for `StatusBarBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/PlatformBehaviors/StatusBar/StatusBarBehavior.shared.cs).
