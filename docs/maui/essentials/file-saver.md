---
title: FileSaver - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: The FileSaver provides the ability to select target folder and save files to the file system.
ms.date: 12/11/2022
---

# FileSaver

The `FileSaver` provides the ability to select a target folder and save files to the file system.

![Screenshot of an FileSaver on macOS](../images/essentials/file-saver-mac.png "FileSaver on macOS")

The following preconditions are required for the `FileSaver`:
# [Android](#tab/android)

If your target device API level is less than 33 add permissions to `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

When your app targets Android API level 34 and up, no additional permissions are required.

For more information about Android storage permission, please refer to the Android documentation about [Manifest.permission](https://developer.android.com/reference/android/Manifest.permission#WRITE_EXTERNAL_STORAGE)

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

Further reading at [https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_files_user-selected_read-write](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_files_user-selected_read-write)

# [Windows](#tab/windows)

Nothing is needed.

# [Tizen](#tab/tizen)

Add permissions to `tizen-manifest.xml`:

```xml
<privilege>http://tizen.org/privilege/mediastorage</privilege>
<privilege>http://tizen.org/privilege/externalstorage</privilege>
```

---

## Syntax

### C#

The `FileSaver` can be used as follows in C#:

```csharp
async Task SaveFile(CancellationToken cancellationToken)
{
    using var stream = new MemoryStream(Encoding.Default.GetBytes("Hello from the Community Toolkit!"));
    var fileSaverResult = await FileSaver.Default.SaveAsync("test.txt", stream, cancellationToken);
    if (fileSaverResult.IsSuccessful)
    {
        await Toast.Make($"The file was saved successfully to location: {fileSaverResult.FilePath}").Show(cancellationToken);
    }
    else
    {
        await Toast.Make($"The file was not saved successfully with error: {fileSaverResult.Exception.Message}").Show(cancellationToken);
    }
}
```

or in case the file is rather big and takes some time to be saved, you may be interested to know the progress:

```csharp
async Task SaveFile(CancellationToken cancellationToken)
{
    using var stream = new MemoryStream(Encoding.Default.GetBytes("Hello from the Community Toolkit!"));
    var saverProgress = new Progress<double>(percentage => ProgressBar.Value = percentage);
    var fileSaverResult = await FileSaver.Default.SaveAsync("test.txt", stream, saverProgress, cancellationToken);
    if (fileSaverResult.IsSuccessful)
    {
        await Toast.Make($"The file was saved successfully to location: {fileSaverResult.FilePath}").Show(cancellationToken);
    }
    else
    {
        await Toast.Make($"The file was not saved successfully with error: {fileSaverResult.Exception.Message}").Show(cancellationToken);
    }
}
```

## Methods

|Method  |Description  |
|---------|---------|
| SaveAsync | Asks for permission, allows selecting a folder and saving files to the file system. |

### FileSaverResult

The result returned from the `SaveAsync` method. This can be used to verify whether the save was successful, check where the file was saved, and also access any exceptions that may have occurred during the save.

#### Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| FilePath | `string` | The location on the disk where the file was saved. |
| Exception | `Exception` | Gets the `Exception` if the save operation fails. |
| IsSuccessful | `bool` | Gets a value determining whether the operation was successful. |

#### Methods

|Method  |Description  |
|---------|---------|
| EnsureSuccess | Verifies whether the save operation was successful. |

> [!WARNING]
> `EnsureSuccess` will throw an `Exception` if the save operation is unsuccessful.

## Dependency Registration

In case you want to inject a service, you first need to register it.
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

		builder.Services.AddSingleton<IFileSaver>(FileSaver.Default);
        return builder.Build();
    }
}
```

Now you can inject the service like this:

```csharp
public partial class MainPage : ContentPage
{
    private readonly IFileSaver fileSaver;

	public MainPage(IFileSaver fileSaver)
	{
		InitializeComponent();
        this.fileSaver = fileSaver;
	}
	
	public async void SaveFile(object sender, EventArgs args)
	{
		using var stream = new MemoryStream(Encoding.Default.GetBytes("Hello from the Community Toolkit!"));
        var fileSaverResult = await fileSaver.SaveAsync("test.txt", stream, cancellationToken);
        fileSaverResult.EnsureSuccess();
        await Toast.Make($"File is saved: {fileSaverResult.FilePath}").Show(cancellationToken);
	}
}
```

## Examples

You can find an example of `FileSaver` in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Essentials/FileSaverPage.xaml).

## API

You can find the source code for `FileSaver` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Essentials/FileSaver/IFileSaver.shared.cs).
