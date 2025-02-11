---
title: Dialog Fragment Service - .NET MAUI Community Toolkit
author: pictos
description: The DialogFragmentService provides an easy way to control the behavior of Modal pages in Android.
ms.date: 02/01/2025
---

# Dialog Fragment Service

.NET 9.0 introduced a breaking change in how modal pages work in Android - they now use a [`DialogFragment`](https://developer.android.com/reference/android/app/DialogFragment). This breaking change resulted in broken functionality within the .NET MAUI Community Toolkit. The `DialogFragmentService` provides a mechanism to fix the breaking changes,

`IDialogFragmentService` is an interface that allows developers to customize the behavior and appearence of Modal pages in .NET MAUI for Android. The .NET MAUI Community Toolkit provides a default implementation to make sure its features, like `StatusBarColor` will work with the new Modal implementation.

## Usage

By default the .NET MAUI Community Toolkit registers the `DialogFragmentService`, but you can control that as follows

```csharp
public static class MauiProgram
{

 public static MauiApp CreateMauiApp()
 {
  var builder = MauiApp.CreateBuilder()
        .UseMauiCommunityToolkit(static options =>
        {
            options.SetShouldUseStatusBarBehaviorOnAndroidModalPage(false);
        });
        return builder.Build();
    }
}
```

There will be cases where you want to fix and customize the `DialogFragment` to match your apps needs, in these scenarios you can create your own implementation of the `IDialogFragmentService` interface and use in combination with other implementations.

## Create you own service

The following example shows how to present the modals in immersive mode. In order to achieve this we need to have access to the `DialogFragment` and configure its `Window` to behave in the required way.

For that, first we will need to create a class that implements the `IDialogFragmentService` interface and customize the method that we need. And make sure this class will only compile for android, otherwise it will fail to build other targets.

```csharp
sealed class MyDialogFragmentService : IDialogFragmentService
{
    // Ommiting other methods
    
    public void OnFragmentStarted(AndroidX.Fragment.App.FragmentManager fm, AndroidX.Fragment.App.Fragment f)
    {
        if (f is not DialogFragment dialogFragment)
        {
            return;
        }

        if (dialogFragment is not { Dialog.Window: { } window })
        {
            return;
        }
        
        if (OperatingSystem.IsAndroidVersionAtLeast(30))
        {
           window.SetDecorFitsSystemWindows(false);
           window.InsetsController?.Hide(WindowInsets.Type.SystemBars());
           if (window.InsetsController is not null)
           {
                window.InsetsController.SystemBarsBehavior = (int)WindowInsetsControllerBehavior.ShowTransientBarsBySwipe;
           }
        }
        else
        {
           SystemUiFlags systemUiVisibility = (SystemUiFlags)window.DecorView.SystemUiVisibility;
           systemUiVisibility |= SystemUiFlags.HideNavigation;
           systemUiVisibility |= SystemUiFlags.Immersive;
           window.DecorView.SystemUiVisibility = (StatusBarVisibility)systemUiVisibility;
        }
    }
}
```

After implementing what is needed it's time to register it into the fragment lifecycle callback, the place to do it is inside the `MauiApp` builder. Here's the code snippet:

```csharp
public static class MauiProgram
{

 public static MauiApp CreateMauiApp()
 {
    var builder = MauiApp.CreateBuilder()
    builder.ConfigureLifecycleEvents(static lifecycleBuilder =>
    {
        lifecycleBuilder.AddAndroid(static androidBuilder =>
        {
            androidBuilder.OnCreate(static (activity, _) =>
            {
                if (activity is not AndroidX.AppCompat.App.AppCompatActivity componentActivity)
                {
                    return;
                }

                if (componentActivity.GetFragmentManager() is not AndroidX.Fragment.App.FragmentManager fragmentManager)
                {
                    return;
                }

                fragmentManager.RegisterFragmentLifecycleCallbacks(new FragmentLifecycleManager(new MyDialogFragmentService()), false);
            });
        });
    });
        return builder.Build();
    }
}
```

And now, all modals will be showed in full-screen mode.

## API

You can find the source code for `IDialogFragmentService` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Interfaces/IDialogFragmentService.android.cs) and about the `FragmentLifecycleManager` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Services/FragmentLifecycleManager.android.cs).
