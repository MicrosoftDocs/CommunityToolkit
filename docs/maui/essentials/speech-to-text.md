---
title: SpeechToText - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: The SpeechToText provides the ability to convert speech to text.
ms.date: 26/05/2023
---

# SpeechToText

The `SpeechToText` API provides the ability to convert speech to text.

![Screenshot of SpeechText implemented on macOS](../images/essentials/speech-to-text-mac.gif "SpeechToText on macOS")

The following preconditions required for the `SpeechToText`:
# [Android](#tab/android)

Add permissions to `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

# [iOS/MacCatalyst](#tab/ios)

Add permissions to `Info.plist`

```xml
<key>NSSpeechRecognitionUsageDescription</key>  
<string>SpeechToText requires speech recognition usage</string>  
<key>NSMicrophoneUsageDescription</key>  
<string>SpeechToText requires microphone usage</string> 
```

# [Windows](#tab/windows)

Add permissions to `Package.appxmanifest`

```xml
<Capabilities>
    <DeviceCapability Name="microphone" />
</Capabilities>
```

# [Tizen](#tab/tizen)

Add permissions to `tizen-manifest.xml`:

```xml
<privilege>http://tizen.org/feature/microphone</privilege>
```

---

## Syntax

### C#

The `SpeechToText` can be used as follows in C#:

```csharp
async Task Listen(CancellationToken cancellationToken)
{
    var isGranted = await speechToText.RequestPermissions(cancellationToken);
    if (!isGranted)
    {
        await Toast.Make("Permission not granted").Show(CancellationToken.None);
        return;
    }

    var recognitionResult = await speechToText.ListenAsync(
                                        CultureInfo.GetCultureInfo(Language),
                                        new Progress<string>(partialText =>
                                        {
                                            RecognitionText += partialText + " ";
                                        }), cancellationToken);

    if (recognitionResult.IsSuccessful)
    {
        RecognitionText = recognitionResult.Text;
    }
    else
    {
        await Toast.Make(recognitionResult.Exception?.Message ?? "Unable to recognize speech").Show(CancellationToken.None);
    }
}
```

## Methods

|Method  |Description  |
|---------|---------|
| RequestPermissions | Asks for permission. |
| ListenAsync | Starts speech recognition. |

### SpeechToTextResult

The result returned from the `ListenAsync` method. This can be used to verify whether the recognition was successful, and also access any exceptions that may have ocurred during the speech recognition.

#### Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| Text | `string` | The recognized text. |
| Exception | `Exception` | Gets the `Exception` if the speech recognition operation failed. |
| IsSuccessful | `bool` | Gets a value determining whether the operation was successful. |

#### Methods

|Method  |Description  |
|---------|---------|
| EnsureSuccess | Verifies whether the speech to text operation was successful. |

> [!WARNING]
> `EnsureSuccess` will throw an `Exception` if the recognition operation was unsuccessful.

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

		builder.Services.AddSingleton<ISpeechToText>(SpeechToText.Default);
        return builder.Build();
    }
}
```

Now you can inject the service like this:

```csharp
public partial class MainPage : ContentPage
{
    private readonly ISpeechToText speechToText;

	public MainPage(ISpeechToText speechToText)
	{
		InitializeComponent();
        this.speechToText = speechToText;
	}
	
	public async void Listen(object sender, EventArgs args)
	{
		var isGranted = await speechToText.RequestPermissions(cancellationToken);
        if (!isGranted)
        {
            await Toast.Make("Permission not granted").Show(CancellationToken.None);
            return;
        }

        var recognitionResult = await speechToText.ListenAsync(
                                            CultureInfo.GetCultureInfo("uk-ua"),
                                            new Progress<string>(), cancellationToken);

        recognitionResult.EnsureSuccess();
        await Toast.Make($"RecognizedText: {recognitionResult.Text}").Show(cancellationToken);
	}
}
```

## Examples

You can find an example of `SpeechToText` in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Essentials/SpeechToTextPage.xaml).

## API

You can find the source code for `SpeechToText` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Interfaces/ISpeechToText.shared.cs).
