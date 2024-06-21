---
title: Getting Started with Native Library Interop
author: miparker, rachelkang
description: Getting Started with Native Library Interop using the starter template and build tasks from Maui.NativeLibraryInterop.
ms.date: 06/18/2024
---

# Getting Started with Native Library Interop

This article covers how to get started with creating a slim binding using Maui.NativeLibraryInterop to simplify the setup. Due to the unique nature of each native library, we are unable to provide a detailed step-by-step walkthrough; rather, these instructions outline the basic steps, key decision points, and guiding examples.

## Prerequisites

Install prerequisites:

- [.NET 8.0 SDK](https://dotnet.microsoft.com/download)
- [.NET MAUI workload](https://github.com/dotnet/core/blob/main/release-notes/6.0/install-maui.md#cli-installation) (via Visual Studio or CLI ```dotnet workload install maui```)
- [Android SDK](https://developer.android.com/tools)
- [Android Studio](https://developer.android.com/studio)
- [Objective-Sharpie](https://aka.ms/objective-sharpie)
    - [Xamarin.iOS](https://download.visualstudio.microsoft.com/download/pr/ceb0ea3f-4db8-46b4-8dc3-8049d27c0107/3960868aa9b1946a6c77668c3f3334ee/xamarin.ios-16.4.0.23.pkg)
- [Visual Studio](https://visualstudio.microsoft.com/downloads/) or [Visual Studio Code](https://code.visualstudio.com/download)
- [Xcode](https://developer.apple.com/xcode/)
- [Xcode Command Line Tools](https://developer.apple.com/download/all/?q=command%20line%20tools) (```xcode-select --install```)

> [!NOTE]
> 
> It's possible to install the [Android SDK](https://developer.android.com/tools) and/or the [Xcode Command Line Tools](https://developer.apple.com/download/all/?q=command%20line%20tools) in a standalone manner. However, installation of the [Xcode Command Line Tools](https://developer.apple.com/download/all/?q=command%20line%20tools) is typically handled via [Xcode](https://developer.apple.com/xcode/). Likewise, [Android SDK](https://developer.android.com/tools) installation is also typically handled via [Android Studio](https://developer.android.com/studio) and/or the [.NET MAUI VS Code Extension](https://aka.ms/mauidevkit-marketplace) as-per the [.NET MAUI Getting Started](https://learn.microsoft.com/dotnet/maui/get-started/installation?view=net-maui-8.0&tabs=visual-studio-code#install-visual-studio-code-and-the-net-maui-extension) documentation.

## Create a new binding

### Set up native binding library

// mention newBinding template and the simple edits that can be made there
// using the NuGet - referencing in csproj

#### [Android](#tab/Android)

`dotnet new android-bindinglib`
// link to docs

#### [iOS & Mac Catalyst](#tab/MaciOS)

`dotnet new iosbinding`
// link to docs

### Create API interface

// mention newBinding template and the simple edits that can be made there

#### [Android](#tab/Android)

// instructions for Android Studio project creation
// Java file - APIs here

#### [iOS & Mac Catalyst](#tab/MaciOS)

// instructions for Xcode project creation
// Swift file - APIs here
// copying ApiDefinitions over

### Consume the APIs in your .NET MAUI app

// mention newBinding template and the simple edits that can be made there
// csproj references


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

> NOTE: Slim wrapper API types which will be used by the .NET Binding must be declared as `public` and need to be annoted with `@objc(NameOfType)` and methods also need to be `public`, and can also benefit from similar annotations `@objc(methodName:parameter1:)` where the name and parameters are specified which help influence the binding which objective sharpie will generate.

You can see in this method that the public API surface only uses types which iOS for .NET already is aware of: `NSData`, `String`, `NSError` and a callback.

In the `Firebase.MaciOS.Binding` project, the `ApiDefinitions.cs` file contains the binding definition for this slim wrapper API:

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

The other half will be to update the `ApiDefinitions.cs` file in the binding project to expose this new method.  There are two ways you can go about this:

1. You can manually add the required code
2. When the binding project builds, objective sharpie is run and an `ApiDefinitions.cs` file is generated inside of the `native/macios/bin/sharpie` folder (this path will vary based on the project you are working on of course).  You can try to find the relevant changes from this file and copy them over manually, or try copying over the whole file and looking at the diff to find the part you need.

In this case, the changes to `ApiDefinitions.cs` would be:

```csharp
[Static]
[Export("unregister:")]
[Async]
void UnRegister(Action completion);
```

Once you've made these changes, you can rebuild the Binding project, and the new API will be ready to use from your .NET MAUI project.

> NOTE: Binding projects for Mac/iOS are not using source generators, and so the project system and inteillisense may not know about the new API's until you've rebuilt the binding project, and reload the solution so that the project reference picks up the newer assembly which was built.  Your app project should still compile regardless of intellisense errors.

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

You can see in this method that the public API surface only uses types which Android for .NET already is aware of: `Activity` and `Boolean`.

In the `Facebook.Android.Binding` project, the `Transforms/Metadata.xml` file contains only some xml to describe how to map the java package name (`com.microsoft.mauifacebook`) to a more C# friendly namespace (`Facebook`).  Generally android bindings are more 'automatic' than  Mac/iOS at this point, and you rarely should need to make changes to these transform files.

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

From this simple change, binding project requires no updates to the `Transforms/Metadata.xml` or other files.  You can simply rebuild the Binding project, and the new API will be ready to use from your .NET MAUI project.

> NOTE: Binding projects for Android are not using source generators, and so the project system and inteillisense may not know about the new API's until you've rebuilt the binding project, and reload the solution so that the project reference picks up the newer assembly which was built.  Your app project should still compile regardless of intellisense errors.
