---
title: FileSaver - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: The FileSaver provides the ability to select target folder and save files to the file system.
ms.date: 12/11/2022
---

# FileSaver

The `FileSaver` provides the ability to select target folder and save files to the file system.

![Screenshot of an FileSaver on macOS](../images/essentials/file-saver-mac.png "FileSaver on macOS")

The following preconditions required for the `FileSaver`:
# [Android](#tab/android)

Add permissions to `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

# [iOS/MacCatalyst](#tab/ios)

Nothing is needed.

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
    try
    {
        var fileLocation = await FileSaver.Default.SaveAsync("test.txt", stream, cancellationToken);
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
        var fileLocation = await fileSaver.SaveAsync("test.txt", stream, cancellationToken);
        await Toast.Make($"File is saved: {fileLocation}").Show(cancellationToken);
	}
}
```

## Examples

You can find an example of `FileSaver` in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Essentials/FileSaverPage.xaml).

## API

You can find the source code for `FileSaver` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Interfaces/IFileSaver.shared.cs).
