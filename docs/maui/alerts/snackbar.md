---
title: Snackbar - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The Snackbar is a timed alert that appears at the bottom of the screen by default."
ms.date: 03/30/2022
---

# Snackbar

The `Snackbar` is a timed alert that appears at the bottom of the screen by default. It is dismissed after a configurable duration of time. `Snackbar` is fully customizable and can be anchored to any `IView`.

The `Snackbar` informs users of a process that an app has performed or will perform. It appears temporarily, towards the bottom of the screen.

## Platform specific initialization

To access the `Snackbar` functionality, the following platform specific setup is required.

<!-- markdownlint-disable MD025 -->
### [Android](#tab/android)

No setup is required.

### [iOS/Mac Catalyst](#tab/macios)

No setup is required.

### [Windows](#tab/windows)

When using `Snackbar` it is essential to perform the following two steps:

#### 1. Enable the snackbar usage with the MauiAppBuilder

When using the `UseMauiCommunityToolkit` make use of the `options` parameter to enable the snackbar usage on windows as follows:

```csharp
var builder = MauiApp.CreateBuilder()
  .UseMauiCommunityToolkit(options =>
  {
    options.SetShouldEnableSnackbarOnWindows(true);
  })
```

The above will automatically register the required handlers by configuring lifecycle events (OnLaunched and OnClosed).

#### 2. Include ToastNotification registrations in your Package.appxmanifest file

To handle the snackbar actions you will need to modify the `Platform\Windows\Package.appxmanifest` file as follows:

1. In **Package.appxmanifest**, in the opening `<Package>` tag, add the following XML Namespaces:

```xml
xmlns:com="http://schemas.microsoft.com/appx/manifest/com/windows10"
xmlns:desktop="http://schemas.microsoft.com/appx/manifest/desktop/windows10"
```

2. In **Package.appxmanifest**, also in the opening `<Package>` tag, update `IgnorableNamespaces` to include `uap` `rescap` `com` and `desktop`:

```xml
IgnorableNamespaces="uap rescap com desktop"
```

##### Example:Completed `<Package>` Tag

Here is an example of a completed opening `<Package>` tag that has added support for `Snackbar`:

```xml
<Package
     xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
     xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
     xmlns:rescap="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities"
     xmlns:com="http://schemas.microsoft.com/appx/manifest/com/windows10"
     xmlns:desktop="http://schemas.microsoft.com/appx/manifest/desktop/windows10"
     IgnorableNamespaces="uap rescap com desktop">
```

3. In **Package.appxmanifest**, inside of each `<Application>` tag, add the following extensions:

```xml
<Extensions>

  <!--Specify which CLSID to activate when notification is clicked-->
   <desktop:Extension Category="windows.toastNotificationActivation">
       <desktop:ToastNotificationActivation ToastActivatorCLSID="6e919706-2634-4d97-a93c-2213b2acc334" /> 
   </desktop:Extension>

   <!--Register COM CLSID-->
   <com:Extension Category="windows.comServer">
       <com:ComServer>
           <com:ExeServer Executable="YOUR-PATH-TO-EXECUTABLE" DisplayName="$targetnametoken$" Arguments="----AppNotificationActivated:"> <!--Example path to executable: CommunityToolkit.Maui.Sample\CommunityToolkit.Maui.Sample.exe-->
               <com:Class Id="6e919706-2634-4d97-a93c-2213b2acc334" />
           </com:ExeServer>
       </com:ComServer>
   </com:Extension>

</Extensions>
```

##### Example: Completed `<Applications>` tag

Here is an example of a completed `<Applications>` tag that now has added support for `Snackbar` ***:

```xml
<Applications>
  <Application Id="App" Executable="$targetnametoken$.exe" EntryPoint="$targetentrypoint$">
      <uap:VisualElements
          DisplayName="$placeholder$"
          Description="$placeholder$"
          Square150x150Logo="$placeholder$.png"
          Square44x44Logo="$placeholder$.png"
          BackgroundColor="transparent">
           <uap:DefaultTile Square71x71Logo="$placeholder$.png" Wide310x150Logo="$placeholder$.png" Square310x310Logo="$placeholder$.png" />
           <uap:SplashScreen Image="$placeholder$.png" />
       </uap:VisualElements>
       <Extensions>

         <desktop:Extension Category="windows.toastNotificationActivation">
             <desktop:ToastNotificationActivation ToastActivatorCLSID="6e919706-2634-4d97-a93c-2213b2acc334" /> 
         </desktop:Extension>
      
         <com:Extension Category="windows.comServer">
             <com:ComServer>
                 <com:ExeServer Executable="YOUR-PATH-TO-EXECUTABLE" DisplayName="$targetnametoken$" Arguments="----AppNotificationActivated:"> <!--Example path to executable: CommunityToolkit.Maui.Sample\CommunityToolkit.Maui.Sample.exe-->
                     <com:Class Id="6e919706-2634-4d97-a93c-2213b2acc334" />
                  </com:ExeServer>
              </com:ComServer>
          </com:Extension>

       </Extensions>
   </Application>
</Applications>
```

##### Example: Updated `Package.appxmanifest` File to Support `Snackbar`

Below is an example `Package.appxmanifest` file that has been updated to support `Snackbar` on Windows:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Package
    xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
    xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
    xmlns:rescap="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities"
    xmlns:com="http://schemas.microsoft.com/appx/manifest/com/windows10"
    xmlns:desktop="http://schemas.microsoft.com/appx/manifest/desktop/windows10"
    IgnorableNamespaces="uap rescap com desktop">

    <Identity Name="maui-package-name-placeholder" Publisher="CN=Microsoft" Version="0.0.0.0" />

    <Properties>
        <DisplayName>$placeholder$</DisplayName>
        <PublisherDisplayName>Microsoft</PublisherDisplayName>
        <Logo>$placeholder$.png</Logo>
    </Properties>

    <Dependencies>
        <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.17763.0" MaxVersionTested="10.0.19041.0" />
        <TargetDeviceFamily Name="Windows.Desktop" MinVersion="10.0.17763.0" MaxVersionTested="10.0.19041.0" />
    </Dependencies>

    <Resources>
        <Resource Language="x-generate" />
    </Resources>

    <Applications>
        <Application Id="App" Executable="$targetnametoken$.exe" EntryPoint="$targetentrypoint$">
            <uap:VisualElements
                DisplayName="$placeholder$"
                Description="$placeholder$"
                Square150x150Logo="$placeholder$.png"
                Square44x44Logo="$placeholder$.png"
                BackgroundColor="transparent">
                <uap:DefaultTile Square71x71Logo="$placeholder$.png" Wide310x150Logo="$placeholder$.png" Square310x310Logo="$placeholder$.png" />
                <uap:SplashScreen Image="$placeholder$.png" />
            </uap:VisualElements>
            <Extensions>

               <desktop:Extension Category="windows.toastNotificationActivation">
                   <desktop:ToastNotificationActivation ToastActivatorCLSID="6e919706-2634-4d97-a93c-2213b2acc334" /> 
               </desktop:Extension>
            
               <com:Extension Category="windows.comServer">
                   <com:ComServer>
                       <com:ExeServer Executable="YOUR-PATH-TO-EXECUTABLE" DisplayName="$targetnametoken$" Arguments="----AppNotificationActivated:"> <!--Example path to executable: CommunityToolkit.Maui.Sample\CommunityToolkit.Maui.Sample.exe-->
                           <com:Class Id="6e919706-2634-4d97-a93c-2213b2acc334" />
                        </com:ExeServer>
                    </com:ComServer>
                </com:Extension>

            </Extensions>
        </Application>
    </Applications>

    <Capabilities>
        <rescap:Capability Name="runFullTrust" />
    </Capabilities>

</Package>
```

For more information on handling activation: [Send a local toast notification from C# apps](/windows/apps/design/shell/tiles-and-notifications/send-local-toast?tabs=uwp#step-3-handling-activation)

### [Tizen](#tab/tizen)

No setup is required.

-----
<!-- markdownlint-enable MD025 -->

## Syntax

The `Snackbar` is invoked using C#.

### C#

To display `Snackbar` you need to create it, using the static method `Make`:

```csharp
using CommunityToolkit.Maui.Alerts;

CancellationTokenSource cancellationTokenSource = new CancellationTokenSource();

var snackbarOptions = new SnackbarOptions
{
    BackgroundColor = Colors.Red,
    TextColor = Colors.Green,
    ActionButtonTextColor = Colors.Yellow,
    CornerRadius = new CornerRadius(10),
    Font = Font.SystemFontOfSize(14),
    ActionButtonFont = Font.SystemFontOfSize(14),
    CharacterSpacing = 0.5
};

string text = "This is a Snackbar";
string actionButtonText = "Click Here to Dismiss";
Action action = async () => await DisplayAlert("Snackbar ActionButton Tapped", "The user has tapped the Snackbar ActionButton", "OK");
TimeSpan duration = TimeSpan.FromSeconds(3);

var snackbar = Snackbar.Make(text, action, actionButtonText, duration, snackbarOptions);

await snackbar.Show(cancellationTokenSource.Token);
```

When calling `Snackbar.Make()`, its parameter `string text` is required. All other parameters are optional.

The following screenshot shows the resulting Snackbar:
# [Android](#tab/android)

![Screenshot of an Snackbar on Android](../images/alerts/snackbar-android.gif "Snackbar on Android")

# [iOS](#tab/ios)

![Screenshot of an Snackbar on iOS](../images/alerts/snackbar-ios.gif "Snackbar on iOS")

---

There is also an extension method, which will anchor the `Snackbar` to any `VisualElement`:

```csharp
await MyVisualElement.DisplaySnackbar("Snackbar is awesome. It is anchored to MyVisualElement");
```

> [!WARNING]
> `Snackbar` on Windows can't be anchored to `VisualElement` and is always displayed as a default Windows Notification.

`SnackBar` contains two events:

- `public static event EventHandler Shown`
- `public static event EventHandler Dismissed`

It also contains the property `public static bool IsShown { get; }`.

```csharp
Snackbar.Shown += (s, e) => { Console.WriteLine(Snackbar.IsShown); };
Snackbar.Dismissed += (s, e) => { Console.WriteLine(Snackbar.IsShown); };
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| Text | `string` | Text message. **Required** |
| Action | `Action` | Action to invoke on action button click. |
| ActionButtonText | `string` | Action button text. |
| Anchor | `IView` | `Snackbar` anchor. `Snackbar` appears near this view. When `null`, the `Snackbar` will appear at the bottom of the screen. |
| Duration | `TimeSpan` | `Snackbar` duration. |
| VisualOptions | `SnackbarOptions` | `Snackbar` visual options. |

### SnackbarOptions

The `SnackbarOptions` allows customize the default `Snackbar` style.

#### Properties

|Property  |Type  |Description  |Default value
|---------|---------|---------|---------|
| CharacterSpacing | `double` | Message character spacing. | `0.0d` |
| Font | `Font` | Message font. | `Font.SystemFontOfSize(14)` |
| TextColor | `Color` | Message text color. | `Colors.Black` |
| ActionButtonFont | `Font` | Action button font. | `Font.SystemFontOfSize(14)` |
| ActionButtonTextColor | `Color` | Action button text color. | `Colors.Black` |
| BackgroundColor | `Color` | Background color. | `Colors.LightGray` |
| CornerRadius | `CornerRadius` | Corner radius. | `new CornerRadius(4, 4, 4, 4)` |

## Methods

|Method  |Description  |
|---------|---------|
| Show | Display the requested `Snackbar`. This will dismiss any currently displayed `Snackbar`|
| Dismiss | Dismiss the requested `Snackbar`. |

> [!NOTE]
> You can display only 1 `Snackbar` at the same time. If you call the `Show` method a second time, the first `Snackbar` will automatically be dismissed before the second `Snackbar` is shown.

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Alerts/SnackbarPage.xaml.cs).

## API

You can find the source code for `Snackbar` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Alerts/Snackbar).
