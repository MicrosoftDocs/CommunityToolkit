---
title: SaveFileDialog - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: The FolderPicker provides the ability to select target folder and save files to the file system.
ms.date: 12/11/2022
---

# SaveFileDialog

The `FolderPicker` provides the ability to select target folder and save files to the file system.

![Screenshot of an SaveFileDialog on macOS](../images/essentials/save-file-dialog-mac.png "SaveFileDialog on macOS")

The following preconditions required for the `SaveFileDialog`:
# [Android](#tab/android)

Add permissions to `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

# [Tizen](#tab/tizen)

Add permissions to `tizen-manifest.xml`:

```xml
<privilege>http://tizen.org/privilege/mediastorage</privilege>
<privilege>http://tizen.org/privilege/externalstorage</privilege>
```

## Syntax

### C#

The `SaveFileDialog` can be used as follows in C#:

```csharp
async Task SaveFile(CancellationToken cancellationToken)
{
    using var stream = new MemoryStream(Encoding.Default.GetBytes("Hello from the Community Toolkit!"));
    try
    {
        var fileLocation = await SaveFileDialog.SaveAsync("test.txt", stream, cancellationToken);
        await Toast.Make($"File is saved: {fileLocation}").Show(cancellationToken);
    }
    catch (Exception ex)
    {
        await Toast.Make($"File is not saved, {ex.Message}").Show(cancellationToken);
    }
}
```

## Methods

|Method  |Description  |
|---------|---------|
| SaveAsync | Asks for permission, allows selecting a folder and saving file to the file system. |

## Examples

You can find an example of `SaveFileDialog` in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Essenatials/SaveFileDialogPage.xaml).

## API

You can find the source code for `SaveFileDialog` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Interfaces/ISaveFileDialog.shared.cs).
