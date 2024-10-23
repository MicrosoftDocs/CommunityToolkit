---
title: Getting Started with Native Library Interop
author: rachelkang
description: Getting Started with Native Library Interop using the starter template and build tasks from Maui.NativeLibraryInterop.
ms.date: 06/18/2024
---

# Getting started with Native Library Interop

This article covers how to get started with Native Library Interop using Maui.NativeLibraryInterop to simplify the setup.

These instructions outline the basic steps, key decision points, and guiding examples for creating bindings via Native Library Interop. For further guidance on specific API and implementation details, please refer to documentation for the native SDKs and libraries of interest.

## Prerequisites

Install prerequisites:

- [.NET 8.0 SDK](https://dotnet.microsoft.com/download)
- [.NET MAUI workload](https://github.com/dotnet/core/blob/main/release-notes/6.0/install-maui.md#cli-installation) (via Visual Studio or CLI ```dotnet workload install maui```)
- [Android SDK](https://developer.android.com/tools)
- [Android Studio](https://developer.android.com/studio)
- [Objective-Sharpie](https://aka.ms/objective-sharpie) (used to manually generate the C# APIs)
    - [Xamarin.iOS](https://download.visualstudio.microsoft.com/download/pr/ceb0ea3f-4db8-46b4-8dc3-8049d27c0107/3960868aa9b1946a6c77668c3f3334ee/xamarin.ios-16.4.0.23.pkg) (required for Objective-Sharpie to work)
- [Visual Studio](https://visualstudio.microsoft.com/downloads/) or [Visual Studio Code](https://code.visualstudio.com/download)
- [Xcode](https://developer.apple.com/xcode/)
- [Xcode Command Line Tools](https://developer.apple.com/download/all/?q=command%20line%20tools) (```xcode-select --install```)

> [!NOTE]
>
> It's possible to install the [Android SDK](https://developer.android.com/tools) and/or the [Xcode Command Line Tools](https://developer.apple.com/download/all/?q=command%20line%20tools) in a standalone manner. However, installation of the [Xcode Command Line Tools](https://developer.apple.com/download/all/?q=command%20line%20tools) is typically handled via [Xcode](https://developer.apple.com/xcode/). Likewise, [Android SDK](https://developer.android.com/tools) installation is also typically handled via [Android Studio](https://developer.android.com/studio) and/or the [.NET MAUI VS Code Extension](https://aka.ms/mauidevkit-marketplace) as-per the [.NET MAUI Getting Started](/dotnet/maui/get-started/installation?view=net-maui-8.0&tabs=visual-studio-code#install-visual-studio-code-and-the-net-maui-extension&preserve-view=true) documentation.

## Create a new binding

The easiest way to get started with creating a new binding is by cloning the **template** in the **[Maui.NativeLibraryInterop](https://github.com/CommunityToolkit/Maui.NativeLibraryInterop)** repo and making modifications from there. To better understand the full scope of how Maui.NativeLibraryInterop is currently set up, read more in the [overview documentation](../index.md).

### Set up the .NET binding libraries

The **template** includes starter .NET for Android and .NET for iOS binding libraries.

Update the binding libraries to reflect the target platforms and .NET version as needed in your .NET app.

> [!NOTE]
>
> For example: If you aim to create only an iOS binding using .NET 9, you can:
> 1. Delete the Android binding library at _template/android/NewBinding.Android.Binding_, and
> 1. Update the target framework in _template/macios/NewBinding.MaciOS.Binding/NewBinding.MaciOS.Binding.csproj_ to be set to `net9.0-ios`.

### Set up the native wrapper projects and libraries

The **template** also includes starter Android Studio projects and Xcode projects.

Update the native projects to reflect the target platforms and versions as needed in your .NET app, and include the native libraries of interest with the following steps.

#### Setup: iOS & Mac Catalyst

The Xcode project is located at template/macios/native/NewBinding.

Update the Xcode project to reflect the target platforms and versions as supported in your .NET app.
In the Xcode project, click on the top-level framework, and in **Targets > General**:

1. Add/remove any **Support Destinations** as needed.
1. Adjust the iOS version as needed.

Bring in the native library for iOS and/or MacCatalyst into your Xcode project, through whatever method works best for your library and your needs (e.g., CocoaPods, Swift Package Manager).

#### Setup: Android

The Android Studio project is located at _template/android/native_.

Update the Android Studio project to reflect the target versions supported in your .NET app.

1. Navigate to the _build.gradle.kts (:app)_ file
1. Update the `compileSdk` version as needed

Bring in the Android native library through gradle

1. Add the package dependency in the dependencies block of the _build.gradle.kts (:app)_ file.
1. Add the repository to the `dependencyResolutionManagement` `repositories` block in the _settings.gradle.kts_ file.
1. Sync project with gradle files (via the button in the upper right corner of Android Studio).

### Create the API interface

Create the API interface between your native projects and your .NET binding projects with the following steps.

#### API Definition: iOS & Mac Catalyst

On the native side, make updates in _template/macios/native/NewBinding/NewBinding/DotnetNewBinding.swift_:

1. Add an import statement to import the native library you just added.
1. Write the API definitions for the native library APIs of interest.
1. Ensure the Xcode project builds successfully and you are satisfied with the APIs.

Back on the .NET side, we are now ready to interop with the native library:

1. Run `dotnet build` from _template/macios/NewBinding.MaciOS.Binding_ to test everything is plugged in correctly and good to go.
1. Optionally use objective sharpie to generate an updated ApiDefinitions.cs file that reflects any changes in your swift code.
    1. Run `sharpie xcode -sdks` to get a list of valid target SDK values for the bind command. Select the value that aligns with the platform and version you are targeting to use with the next command, for example `iphoneos18.0`.
    1. Run `sharpie bind` against the header files in the xcframework created by the binding project:
        ```
        cd _template/macios/native/NewBinding/bin/Debug/net9.0-ios/NewBinding.MaciOS.Binding.resources/NewBindingiOS.xcframework/ios-arm64/NewBinding.framework &&
        sharpie bind --output=sharpie-out --namespace=NewBindingMaciOS --sdk=iphoneos18.0 --scope=Headers Headers/NewBinding-Swift.h
        ```
    1. Update the contents of _template/macios/NewBinding.MaciOS.Binding/ApiDefinition.cs_ by replacing it with the contents of _sharpie-out/ApiDefinitions.cs_.
    1. Run `dotnet build` from _template/macios/NewBinding.MaciOS.Binding_ again.

#### API Definition: Android

On the native side, make updates in _template/android/native/app/src/main/java/com/example/newbinding/DotnetNewBinding.java_:

1. Add an import statement to import the native library you just added.
1. Write the API definitions for the native library APIs of interest.
1. Ensure the Android Studio project builds successfully and you are satisfied with the APIs.

Back on the .NET side, we are now ready to interop with the native library:
1. Run `dotnet build` from _template/android/NewBinding.Android.Binding_ to test everything is plugged in correctly and good to go. (Note: This step will require that you have JDK 17 installed)
1. Reference any Android binding dependencies by adding `@(AndroidMavenLibrary)` or `@(PackageReference)` elements to satisfy the java dependency chain for the native library you are binding. (Note: The gradle/maven dependencies often need to be explicitly referenced, as they are not automatically bundled into your library.)

```xml
<ItemGroup Condition="$(TargetFramework.Contains('android'))">
    <AndroidMavenLibrary Include="my.library:dependency-library" Version="1.0.0" Bind="false" />
</ItemGroup>
```

For more information about this process, see the [AndroidMavenLibrary reference](/dotnet/android/binding-libs/advanced-concepts/android-maven-library) documentation.

> [!NOTE]
> You can rename the placeholder ```DotnetNewBinding``` class to better reflect the native library being wrapped. For more examples and tips for writing the API definitions, read more in the section below: [Modify an existing binding](#modify-an-existing-binding).

### Consume the APIs in your .NET app

The **template** includes a .NET MAUI sample app at _template/sample/MauiSample_, which references the .NET binding projects and makes the native libraries immediately ready to use!

If you are interested in using your own .NET MAUI, .NET for Android, .NET for iOS, and/or .NET for Mac Catalyst apps, however, you may do so by modifying your .NET app project files to reference the binding libraries:

```xml
<!-- Reference to MaciOS Binding project -->
<ItemGroup Condition="$(TargetFramework.Contains('ios')) Or $(TargetFramework.Contains('maccatalyst'))">
    <ProjectReference Include="..\..\macios\NewBinding.MaciOS.Binding\NewBinding.MaciOS.Binding.csproj" />
</ItemGroup>

<!-- Reference to Android Binding project -->
<ItemGroup Condition="$(TargetFramework.Contains('android'))">
    <ProjectReference Include="..\..\android\NewBinding.Android.Binding\NewBinding.Android.Binding.csproj" />
</ItemGroup>
```

## Modify an existing binding

If the existing API surface doesn't expose the functionality you need in your own project, it's time to make your own modifications!

### iOS & Mac Catalyst

Inside the Xcode project, you will find one or more Swift files which define the public API surface for the binding. For example, the `register` method for Firebase Messaging is defined as:

```Swift
@objc(MauiFIRMessaging)
public class MauiFIRMessaging : NSObject {

    @objc(register:completion:)
    public static func register(apnsToken: NSData, completion: @escaping (String?, NSError?) -> Void) {
        let data = Data(referencing: apnsToken);
        Messaging.messaging().apnsToken = data
        Messaging.messaging().token(completion: { fid, error in
            completion(fid, error as NSError?)
        })
    }
    // ...
}
```

> [!NOTE]
> Native wrapper API types which will be used by the .NET Binding must be declared as `public` and need to be annoted with `@objc(NameOfType)` and methods also need to be `public`, and can also benefit from similar annotations `@objc(methodName:parameter1:)` where the name and parameters are specified which help influence the binding which objective sharpie will generate.

You can see in this method that the public API surface only uses types which .NET for iOS is already aware of: `NSData`, `String`, `NSError` and a callback.

In the `Firebase.MaciOS.Binding` project, the _ApiDefinitions.cs_ file contains the binding definition for this native wrapper API:

```csharp
using System;
using Foundation;

namespace Firebase
{
    // @interface MauiFIRMessaging : NSObject
    [BaseType (typeof(NSObject))]
    interface MauiFIRMessaging
    {
        [Static]
        [Export ("register:completion:")]
        [Async]
        void Register (NSData apnsToken, Action<string?, NSError?> completion);
        // ...
    }
```

Let's say you want to add a method for unregistering.  The Swift code would look something like this:

```Swift
@objc(unregister:)
public static func unregister(completion: @escaping (NSError?) -> Void) {
    // need delegate to watch for fcmToken updates
    Messaging.messaging().deleteToken(completion: { error in
        completion(error as NSError?)
    })
}
```

The other half will be to update the _ApiDefinitions.cs_ file in the binding project to expose this new method.  There are two ways you can go about this:

1. You can manually add the required code
2. After building the binding project, you can run the objective sharpie tool to generate an _ApiDefinitions.cs_ file.  You can try to find the relevant changes from this file and copy them over manually, or try copying over the whole file and looking at the diff to find the part you need.

In this case, the changes to _ApiDefinitions.cs_ would be:

```csharp
[Static]
[Export("unregister:")]
[Async]
void UnRegister(Action completion);
```

Once you've made these changes, you can rebuild the Binding project, and the new API will be ready to use from your .NET MAUI project.

> [!NOTE]
> Binding projects for Mac/iOS are not using source generators, and so the project system and intellisense may not know about the new API's until you've rebuilt the binding project, and reloaded the solution so that the project reference picks up the newer assembly.  Your app project should still compile regardless of intellisense errors.

### Android

Inside the Android Studio project you will find a module directory which contains a java file definining the public API surface for the binding.  For example, the `initialize` method for Facebook is defined as below:

```java
package com.microsoft.mauifacebook;

import android.app.Activity;
import android.app.Application;
import android.os.Bundle;
import android.util.Log;

import com.facebook.LoggingBehavior;
import com.facebook.appevents.AppEventsLogger;

public class FacebookSdk {

    static AppEventsLogger _logger;

    public static void initialize(Activity activity, Boolean isDebug) {
        Application application = activity.getApplication();

        if (isDebug) {
            com.facebook.FacebookSdk.setIsDebugEnabled(true);
        }

        com.facebook.FacebookSdk.addLoggingBehavior(LoggingBehavior.APP_EVENTS);

        AppEventsLogger.activateApp(application);

        _logger = AppEventsLogger.newLogger(activity);
    }

    // ...
}
```

You can see in this method that the public API surface only uses types which .NET for Android is already aware of: `Activity` and `Boolean`.

In the **Facebook.Android.Binding** project, the _Transforms/Metadata.xml_ file contains only some xml to describe how to map the java package name (`com.microsoft.mauifacebook`) to a more C# friendly namespace (`Facebook`).  Generally android bindings are more 'automatic' than  Mac/iOS at this point, and you rarely should need to make changes to these transform files.

```xml
<metadata>
    <attr path="/api/package[@name='com.microsoft.mauifacebook']" name="managedName">Facebook</attr>
</metadata>
```

Let's say you want to add a method for logging an event.  The java code would look something like this:

```java
public static void logEvent(String eventName) {
    _logger.logEvent(eventName);
}
```

From this simple change, binding project requires no updates to the _Transforms/Metadata.xml_ or other files.  You can simply rebuild the Binding project, and the new API will be ready to use from your .NET MAUI project.

> [!NOTE]
> Binding projects for Android are not using source generators, and so the project system and intellisense may not know about the new API's until you've rebuilt the binding project, and reloaded the solution so that the project reference picks up the newer assembly.  Your app project should still compile regardless of intellisense errors.
