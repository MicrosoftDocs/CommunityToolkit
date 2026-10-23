---
title: StatusBarBehavior - .NET MAUI Community Toolkit
author: pictos
description: "The StatusBarBehavior provides the ability to customize the color and style of a device's status bar."
ms.date: 10/23/2026
---

# StatusBarBehavior

The `StatusBarBehavior` provides the ability to customize the color and style of a device's status bar.

The `StatusBarBehavior` applies the color and style values when the properties are updated. The values are also applied based on the `ApplyOn` property, this property makes it possible to define which lifecycle event is used:

- `StatusBarApplyOn.OnBehaviorAttachedTo` - Applies the color and style when the behavior has been attached to a page. **This is the default.**
- `StatusBarApplyOn.OnPageNavigatedTo` - Applies the color and style when the page has been navigated to.

> [!NOTE]
> If your application changes the status bar appearance on a per page basis then you should make use of the `StatusBarApplyOn.OnPageNavigatedTo` value for the `ApplyOn` property. Otherwise when navigating back the system will preserve the status bar appearance from the page the user navigated from and not to.

> [!NOTE]
> `StatusBarApplyOn.OnPageNavigatedTo` applies nothing when .NET MAUI raises `NavigatedTo` before the page loads. On iOS that is the case when a `TabbedPage` selects the tab of the page and when a `FlyoutPage` shows the page as its `Detail`. With .NET 11, it is also the case when a `NavigationPage` pushes the page, or pops back to it, without animation.

[!INCLUDE [important note on bindings within behaviors](../includes/behavior-bindings.md)]

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

There's another way to access the status bar APIs in C#, you can call the methods directly, as you can see in the snippet below:

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
> If you want to add this code to the `MainPage`'s constructor, `OnAppearing` or `OnNavigatedTo` methods, please use the `Behavior` instead.
> Using directly on these places can crash your application since the platform-specific components may not be initialized.

## Configuration

# [Android](#tab/android)

No changes needed.

To apply the status bar color and style of the activity to modal pages as well, see [Dialog Fragment Service](../platform-specific/DialogFragment-customization.md). That page also describes how a modal page is laid out below the status bar.

# [iOS](#tab/ios)

No changes needed. UIKit takes the style of the status bar from the view controllers of your app, and the toolkit makes them return the style that you set. This works as long as the _Platforms/iOS/Info.plist_ file doesn't turn view controller-based status bar appearance off.

If your _Platforms/iOS/Info.plist_ file contains the following entry, which earlier versions of this page told you to add, remove it:

```xml
    <key>UIViewControllerBasedStatusBarAppearance</key>
    <false/>
```

> [!IMPORTANT]
> In an app that is built with the iOS 27 SDK (Xcode 27) or later, UIKit ignores `UIApplication.SetStatusBarStyle`. With the key set to `false` the style of the status bar then doesn't change, and the toolkit writes the message _Unable to apply the Status Bar Style because Info.plist sets UIViewControllerBasedStatusBarAppearance to false: remove the key from Info.plist_ to the trace output. An app that is built with an earlier SDK still applies the style while the key is `false`, but the key isn't needed there either.

On .NET 10, the first `LightContent` or `DarkContent` that you set makes the view controllers that don't choose a style of their own return the one you set. `Default` gives every view controller its own style back. A view controller that overrides `preferredStatusBarStyle` keeps its own style, and so does `SFSafariViewController`.

-----

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| ApplyOn | StatusBarApplyOn | When to apply the status bar color and style. |
| StatusBarColor | Color | The `Color` name from the Microsoft.Maui.Graphics namespace. |
| StatusBarStyle | StatusBarStyle | The style used by statusbar, can be LightContent, DarkContent or Default. |

## Frequently asked questions

### Why doesn't the status bar style change on iOS?

Look for the message _Unable to apply the Status Bar Style because Info.plist sets UIViewControllerBasedStatusBarAppearance to false_ in the trace output. If it's there, remove the `UIViewControllerBasedStatusBarAppearance` key from the _Platforms/iOS/Info.plist_ file, as described in [Configuration](#configuration). If it isn't, check whether a view controller that overrides `preferredStatusBarStyle` is on screen: it keeps its own style.

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/StatusBarBehaviorPage.xaml).

## API

You can find the source code for `StatusBarBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/PlatformBehaviors/StatusBar/StatusBarBehavior.shared.cs).
