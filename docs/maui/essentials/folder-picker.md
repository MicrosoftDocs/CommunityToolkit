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

# [Tizen](#tab/tizen)

Add permissions to `tizen-manifest.xml`:

```xml
<privilege>http://tizen.org/privilege/mediastorage</privilege>
<privilege>http://tizen.org/privilege/externalstorage</privilege>
```

## Syntax

### C#

The `FolderPicker` can be used as follows in C#:

```csharp
async Task PickFolder(CancellationToken cancellationToken)
{
    try
    {
        var folder = await FolderPicker.Default.PickAsync(cancellationToken);
        await Toast.Make($"Folder picked: Name - {folder.Name}, Path - {folder.Path}", ToastDuration.Long).Show(cancellationToken);
    }
    catch (Exception ex)
    {
        await Toast.Make($"Folder is not picked, {ex.Message}").Show(cancellationToken);
    }
}
```

### Folder

The `Folder` record represents a folder in the file system. It defines the following properties:

- Path contains a Folder path.
- Name contains a Folder name.

## Methods

|Method  |Description  |
|---------|---------|
| PickAsync | Asks for permission and allows selecting a folder in the file system. |

## Examples

You can find an example of `FolderPicker` in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Essentials/FolderPickerPage.xaml).

## API

You can find the source code for `FolderPicker` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Interfaces/IFolderPicker.shared.cs).
