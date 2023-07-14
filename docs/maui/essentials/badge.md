---
title: Badge - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: The Badge allows developers to set the app icon badge number on the homescreen.
ms.date: 07/14/2023
---

# Badge

The `Badge` allows developers to set the app icon badge number on the homescreen.

![Screenshot of an Badge on Windows](../images/essentials/badge-windows.png "Badge on Windows")

---

The following preconditions required for the `Badge`:

# [iOS/MacCatalyst](#tab/ios)

Authorize Badge permission for the app. It is automatically requested.

# [Tizen](#tab/tizen)

Add permissions to `tizen-manifest.xml`:

```xml
<privilege>http://tizen.org/privilege/notification</privilege>
```

## Syntax

### C#

The `Badge` can be used as follows in C#:

```csharp
void SetCount(uint value)
{
    Badge.Default.SetCount(value);
}
```

## Methods

|Method  |Description  |
|---------|---------|
| SetCount | Set the badge count. |

## Dependency Registration

In case you want to inject service, you first need to register it.
Update `MauiProgram.cs` with the next changes:

```csharp
public static class MauiProgram
{
    public static MauiApp CreateMauiApp()
    {
        var builder = MauiApp.CreateBuilder();
        builder
            .UseMauiApp<App>()
			.UseMauiCommunityToolkit();

		builder.Services.AddSingleton<IBadge>(Badge.Default);
        return builder.Build();
    }
}
```

Now you can inject the service like this:

```csharp
public partial class MainPage : ContentPage
{
    private readonly IBadge badge;

	public MainPage(IBadge badge)
	{
		InitializeComponent();
        this.badge = badge;
	}
	
	public void SetCount(uint value)
    {
        badge.SetCount(value);
    }
}
```

## Examples

You can find an example of `Badge` in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Essentials/BadgePage.xaml).

## API

You can find the source code for `Badge` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Essentials/Badge/IBadge.shared.cs).

## Android

In the world of Android, one size rarely fits all. This principle holds true when it comes to setting application badge counts, due to the lack of a standardized API provided by Android system for this functionality.

Different Android launchers have chosen to implement badge counts in their unique way. Most launchers including popular ones like Nova Launcher, Microsoft Launcher, etc., have their specific methods to handle this feature.

Consequently, to ensure that your application's badge notifications appear correctly across these diverse launchers, you must resort to programming specific code implementations for each launcher. This means adapting your code to the specific requirements of each launcher's unique badge count-indicating mechanism.

Consider it as a hurdle that developers must overcome, in the path towards achieving a universal application experience. This is due to Android's flexible ecosystem that encourages diversity and customization.

It's important to note that while it's feasible to cover the most popular Android launchers, it would be almost impossible to cater to every single one, given the sheer number of launchers available in the market.

With the CommunityToolkit we provide you the way implement your own badge counter logic for providers you want to support. This is how you can do that:

1. Implement `CommunityToolkit.Maui.ApplicationModel.IBadgeProvider` interface. See `SamsungBadgeProvider` implementation as example: [SamsungBadgeProvider](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Platforms/Android/SamsungBadgeProvider.cs).
1. In the Android `MainApplication` constructor map launcher identifier with your `BadgeProvider` implementation". For example for Samsung launcher it should look like this:
```csharp
public MainApplication(IntPtr handle, JniHandleOwnership ownership)
		: base(handle, ownership)
	{
		var samsungProvider = new SamsungBadgeProvider();
		BadgeFactory.SetBadgeProvider("com.sec.android.app.launcher", samsungProvider);
		BadgeFactory.SetBadgeProvider("com.sec.android.app.twlauncher", samsungProvider);
	}
```
1. Add required permissions to the `AndroidManifest.xaml`.  For example for Samsung launcher it should look like this:
```xml
<uses-permission android:name="com.sec.android.provider.badge.permission.READ" />
<uses-permission android:name="com.sec.android.provider.badge.permission.WRITE" />
```
