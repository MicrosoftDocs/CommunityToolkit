---
title: FolderPicker - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: The FolderPicker provides the ability to pick a folder from the file system.
ms.date: 12/11/2022
---

# FolderPicker

The `FolderPicker` provides the ability to pick a folder from the file system.

The following preconditions required for the `FolderPicker`:
# [Android](#tab/android)

Add permissions to `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

# [iOS](#tab/ios)

Nothing is needed.

# [MacCatalyst](#tab/macos)

When using [App Sandbox](https://developer.apple.com/documentation/security/app_sandbox), which is required if you wish to distribute your macOS application via the Apple App Store, you will also need to enable [Accessing files from the macOS App Sandbox](https://developer.apple.com/documentation/security/app_sandbox/accessing_files_from_the_macos_app_sandbox).

There are two key options when enabling access to files from the macOS App Sandbox:

1. Read-only access

Add the following into your entitlements.plist file:

```xml
<key>com.apple.security.files.user-selected.read-only</key>
<true/>
```

Further reading at: [https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_files_user-selected_read-only](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_files_user-selected_read-only)

2. Read-write access

Add the following into your entitlements.plist file:

```xml
<key>com.apple.security.files.user-selected.read-write</key>
<true/>
```

Further reading at: [https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_files_user-selected_read-write](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_files_user-selected_read-write)

# [Windows](#tab/windows)

Nothing is needed.

# [Tizen](#tab/tizen)

Add permissions to `tizen-manifest.xml`:

```xml
<privilege>http://tizen.org/privilege/mediastorage</privilege>
<privilege>http://tizen.org/privilege/externalstorage</privilege>
```

---

## Basic usage

The `FolderPicker` can be added to a .NET MAUI application in the following way.

### Request permissions

Developers must manually request Permissions.StorageRead and/or Permissions.StorageWrite:

```csharp
var readPermissionsRequest = await Permissions.RequestAsync<Permissions.StorageRead>();
var writePermissionsRequest = await Permissions.RequestAsync<Permissions.StorageWrite>();
```

StorageWrite permission is required in case you plan to write something in the folder.

### Pick folder

```csharp
async Task PickFolder(CancellationToken cancellationToken)
{
    var result = await FolderPicker.Default.PickAsync(cancellationToken);
    if (result.IsSuccessful)
    {
        await Toast.Make($"The folder was picked: Name - {result.Folder.Name}, Path - {result.Folder.Path}", ToastDuration.Long).Show(cancellationToken);
    }
    else
    {
        await Toast.Make($"The folder was not picked with error: {result.Exception.Message}").Show(cancellationToken);
    }
}
```

### Folder

The `Folder` record represents a folder in the file system. It defines the following properties:

- Path contains a Folder path.
- Name contains a Folder name.

### FolderPickerResult

Stores information from `PickAsync`.

#### Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| Folder | `Folder` | Gets the `Folder` that represents the selected folder in the file system. |
| Exception | `Exception` | Gets the `Exception` if the pick operation failed. |
| IsSuccessful | `bool` | Gets a value determining whether the operation was successful. |

#### Methods

|Method  |Description  |
|---------|---------|
| EnsureSuccess | Verifies whether the pick operation was successful. |

> [!WARNING]
> `EnsureSuccess` will throw an `Exception` if the pick operation was unsuccessful.

## Methods

|Method  |Description  |
|---------|---------|
| PickAsync | Asks for permission and allows selecting a folder in the file system. |

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

        // Register the FolderPicker as a singleton
        builder.Services.AddSingleton<IFolderPicker>(FolderPicker.Default);
        
        // Register the MainPage as transient to make sure it can resolve the IFolderPicker dependency.
        builder.Services.AddTransient<MainPage>();
        return builder.Build();
    }
}
```

Now you can inject the service like this:

```csharp
public partial class MainPage : ContentPage
{
    private readonly IFolderPicker folderPicker;

    public MainPage(IFolderPicker folderPicker)
    {
        InitializeComponent();
        this.folderPicker = folderPicker;
    }

    async Task PickFolder(CancellationToken cancellationToken)
    {
        var result = await folderPicker.PickAsync(cancellationToken);
        result.EnsureSuccess();
        await Toast.Make($"Folder picked: Name - {result.Folder.Name}, Path - {result.Folder.Path}", ToastDuration.Long).Show(cancellationToken);
    }
}
```

For more detail on how to provide a `CancellationToken` refer to the [Microsoft documentation](/dotnet/standard/threading/cancellation-in-managed-threads).

## Examples

You can find an example of `FolderPicker` in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Essentials/FolderPickerPage.xaml).

## API

You can find the source code for `FolderPicker` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Essentials/FolderPicker/IFolderPicker.shared.cs).
