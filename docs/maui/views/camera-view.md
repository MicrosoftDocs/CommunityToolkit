---
title: CameraView - .NET MAUI Community Toolkit
author: bijington
description: "The CameraView provides the ability to connect to a camera, display a preview from the camera, take photos, and record videos."
ms.date: 10/23/2026
---

# CameraView

The `CameraView` provides the ability to connect to a camera, display a preview from the camera, take photos, and record videos. The `CameraView` also offers features to support controlling the flash and torch, adjusting zoom, saving captured media to a file, and offering different hooks for events.

The following sections will incrementally build on how to use the `CameraView` in a .NET MAUI application. They rely on the use of a [`CameraViewModel`](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/ViewModels/Views/CameraView/CameraViewViewModel.cs). that will be set as the `BindingContext` of the example [`CameraViewPage`](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/CameraView/CameraViewPage.xaml).

## Platform specific initialization

The `CameraView` is part of the `CommunityToolkit.Maui.Camera` nuget package. To first use the `CameraView` please refer to the [Getting started](../get-started.md?tabs=CommunityToolkitMauiCamera) section. The following platform specific setup is required.

<!-- markdownlint-disable MD025 -->
<!-- markdownlint-disable MD051 -->
### [Android](#tab/android)

The following permissions need to be added to the `Platforms/Android/AndroidManifest.xml` file:

```xml
<uses-permission android:name="android.permission.CAMERA" />
```

In case you plan to record video, request Microphone permissions:
```xml
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

This should be added inside the `<manifest>` element. Below shows a more complete example:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    <application android:allowBackup="true" android:icon="@mipmap/appicon" android:roundIcon="@mipmap/appicon_round" android:supportsRtl="true" />

    <uses-permission android:name="android.permission.CAMERA" />

    <!--Optional. Only for video recording-->
    <uses-permission android:name="android.permission.RECORD_AUDIO" />

</manifest>
```

### [iOS](#tab/ios)

The following entries need to be added to the `Platforms/iOS/Info.plist` file:

```xml
<key>NSCameraUsageDescription</key>
<string>PROVIDE YOUR REASON HERE</string>
```

In case you plan to record video, request Microphone permissions:
```xml
<key>NSMicrophoneUsageDescription</key>
<string>PROVIDE YOUR REASON HERE</string>
```

This should be added inside the `<dict>` element. Below shows a more complete example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>UIDeviceFamily</key>
    <array>
        <integer>1</integer>
        <integer>2</integer>
    </array>
    <key>UIRequiredDeviceCapabilities</key>
    <array>
        <string>arm64</string>
    </array>
    <key>UISupportedInterfaceOrientations</key>
    <array>
        <string>UIInterfaceOrientationPortrait</string>
        <string>UIInterfaceOrientationLandscapeLeft</string>
        <string>UIInterfaceOrientationLandscapeRight</string>
    </array>
    <key>UISupportedInterfaceOrientations~ipad</key>
    <array>
        <string>UIInterfaceOrientationPortrait</string>
        <string>UIInterfaceOrientationPortraitUpsideDown</string>
        <string>UIInterfaceOrientationLandscapeLeft</string>
        <string>UIInterfaceOrientationLandscapeRight</string>
    </array>
    <key>XSAppIconAssets</key>
    <string>Assets.xcassets/appicon.appiconset</string>

    <key>NSCameraUsageDescription</key>
    <string>PROVIDE YOUR REASON HERE</string>

    <key>NSMicrophoneUsageDescription</key>
    <string>PROVIDE YOUR REASON HERE</string>
</dict>
</plist>
```

### [Mac Catalyst](#tab/mac)

The following entries need to be added to the `Platforms/MacCatalyst/Info.plist` file:

```xml
<key>NSCameraUsageDescription</key>
<string>PROVIDE YOUR REASON HERE</string>
```

In case you plan to record video, request Microphone permissions:
```xml
<key>NSMicrophoneUsageDescription</key>
<string>PROVIDE YOUR REASON HERE</string>
```

This should be added inside the `<dict>` element. Below shows a more complete example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>UIDeviceFamily</key>
    <array>
        <integer>1</integer>
        <integer>2</integer>
    </array>
    <key>UIRequiredDeviceCapabilities</key>
    <array>
        <string>arm64</string>
    </array>
    <key>UISupportedInterfaceOrientations</key>
    <array>
        <string>UIInterfaceOrientationPortrait</string>
        <string>UIInterfaceOrientationLandscapeLeft</string>
        <string>UIInterfaceOrientationLandscapeRight</string>
    </array>
    <key>UISupportedInterfaceOrientations~ipad</key>
    <array>
        <string>UIInterfaceOrientationPortrait</string>
        <string>UIInterfaceOrientationPortraitUpsideDown</string>
        <string>UIInterfaceOrientationLandscapeLeft</string>
        <string>UIInterfaceOrientationLandscapeRight</string>
    </array>
    <key>XSAppIconAssets</key>
    <string>Assets.xcassets/appicon.appiconset</string>

    <key>NSCameraUsageDescription</key>
    <string>PROVIDE YOUR REASON HERE</string>

    <key>NSMicrophoneUsageDescription</key>
    <string>PROVIDE YOUR REASON HERE</string>
</dict>
</plist>
```

More details can be found here: https://developer.apple.com/documentation/avfoundation/requesting-authorization-to-capture-and-save-media

### [Windows](#tab/windows)

No setup is required.

### [Tizen](#tab/tizen)

Tizen is not currently supported.

-----
<!-- markdownlint-enable MD051 -->
<!-- markdownlint-enable MD025 -->

## Basic usage

The `CameraView` can be added to a .NET MAUI application in the following way.

### Request permissions

Developers must manually request Permissions.Camera and/or Permissions.Microphone:

```csharp
var cameraPermissionsRequest = await Permissions.RequestAsync<Permissions.Camera>();
```

In case you plan to record video, request Microphone permissions:

```csharp
var microphonePermissionsRequest = await Permissions.RequestAsync<Permissions.Microphone>();
```

> [!NOTE]
> A `CameraView` can try to start its preview before the camera permission is granted, for example while your app is still asking for it. The failure is reported through the [`ErrorOccurred`](#events) event. On Android, the preview then starts by itself when the app resumes with the permission granted. On the other platforms, call `StartCameraPreview` again once the permission is granted. See [Start preview](#start-preview) for details.

### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.CameraViewPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    
    <Grid ColumnDefinitions="*,*,*" RowDefinitions="*,30">
        <toolkit:CameraView 
            Grid.ColumnSpan="3" 
            Grid.Row="0" />
    </Grid>

</ContentPage>
```

The result will be a surface rendering the output of the default camera connected to the device.

## Access the current camera

The `SelectedCamera` property provides the ability to access the currently selected camera.

The following example shows how to bind the `SelectedCamera` property from the `CameraView` to a property on the `CameraViewModel` with the same name (`SelectedCamera`).

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.CameraViewPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    
    <Grid ColumnDefinitions="*,*,*" RowDefinitions="*,30,30">
        <toolkit:CameraView 
            Grid.ColumnSpan="3" 
            Grid.Row="0" 
            SelectedCamera="{Binding SelectedCamera}" />
    </Grid>

</ContentPage>
```

## Control Zoom

The `SelectedCamera` property provides both a `MinimumZoomFactor` and a `MaximumZoomFactor` property, these are read-only and provide developers with a programmatic way of determining what zoom can be applied to the current camera. In order to change the zoom on the current camera the `CameraView` provides the `ZoomFactor` property.

> [!NOTE]
> If a value is provided outside of the `MinimumZoomFactor` and `MaximumZoomFactor` the `CameraView` will clamp the value to keep it within the bounds.

> [!NOTE]
> On Android, `MinimumZoomFactor` and `MaximumZoomFactor` come from CameraX for each camera, in Debug and in Release (trimmed) apps. Earlier versions reported a range of 1 to 1 for every camera in Release apps ([#2389](https://github.com/CommunityToolkit/Maui/issues/2389)), which clamped every `ZoomFactor` to 1.

The following example shows how to add a `Slider` into the application and setup the following bindings:

- Bind the `Maximum` property of the `Slider` to the `MaximumZoomFactor` of the `SelectedCamera` property.
- Bind the `Minimum` property of the `Slider` to the `MinimumZoomFactor` of the `SelectedCamera` property.
- Bind the `Value` property of the `Slider` to the `CurrentZoom` property on the `CameraViewModel` class.

The final change involves binding the `ZoomFactor` property of the `CameraView` to the `CurrentZoom` property on the `CameraViewModel` class.

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.CameraViewPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    
    <Grid ColumnDefinitions="*,*,*" RowDefinitions="*,30,30">
        <toolkit:CameraView 
            Grid.ColumnSpan="3" 
            Grid.Row="0"
            SelectedCamera="{Binding SelectedCamera}"
            ZoomFactor="{Binding CurrentZoom}" />

        <Slider 
            Grid.Column="0"
            Grid.Row="1"
            Value="{Binding CurrentZoom}"
            Maximum="{Binding SelectedCamera.MaximumZoomFactor, FallbackValue=1}"
            Minimum="{Binding SelectedCamera.MinimumZoomFactor, FallbackValue=1}"/>
    </Grid>

</ContentPage>
```

## Camera Flash Mode

The `CameraView` provides the ability to programmatically change the flash mode on the device, the possible options are:

- `Off` - the flash is off and will **not** be used.
- `On` - the flash is on and will **always** be used.
- `Auto` - the flash will automatically be used based on the lighting conditions.

The `SelectedCamera` property also provides the `IsFlashSupported` which makes it possible to determine whether the currently selected camera has a flash that can be controlled.

The following example shows how to add a `Picker` into the application and setup the following bindings:

- Bind the `IsVisible` property of the `Picker` to the `IsFlashSupported` of the `SelectedCamera` property.
- Bind the `ItemsSource` property of the `Picker` to the `FlashModes` property on the `CameraViewModel` class - a simple list of the possible values of the `CameraFlashMode` enum.
- Bind the `SelectedItem` property of the `Picker` to the `FlashMode` property on the `CameraViewModel` class.

The final change involves binding the `CameraFlashMode` property of the `CameraView` to the `FlashMode` property on the `CameraViewModel` class.

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.CameraViewPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    
    <Grid ColumnDefinitions="*,*,*" RowDefinitions="*,30,30">
        <toolkit:CameraView 
            Grid.ColumnSpan="3" 
            Grid.Row="0"
            SelectedCamera="{Binding SelectedCamera}"
            ZoomFactor="{Binding CurrentZoom}"
            CameraFlashMode="{Binding FlashMode}" />

        <Slider 
            Grid.Column="0"
            Grid.Row="1"
            Value="{Binding CurrentZoom}"
            Maximum="{Binding SelectedCamera.MaximumZoomFactor, FallbackValue=1}"
            Minimum="{Binding SelectedCamera.MinimumZoomFactor, FallbackValue=1}"/>

        <Picker 
            Grid.Column="1"
            Grid.Row="1"
            Title="Flash"
            IsVisible="{Binding Path=SelectedCamera.IsFlashSupported, FallbackValue=false}"
            ItemsSource="{Binding FlashModes}"
            SelectedItem="{Binding FlashMode}" />
    </Grid>

</ContentPage>
```

## ImageCaptureResolution

The `CameraView` provides the ability to programmatically change resolution for images captured from the current camera.

> [!NOTE]
> This will not change the resolution displayed in the preview from the camera.

The `SelectedCamera` property also provides the `SupportedResolutions` which makes it possible to determine which resolutions the current camera supports.

The following example shows how to add a `Picker` into the application and setup the following bindings:

- Bind the `ItemsSource` property of the `Picker` to the `SupportedResolutions` of the `SelectedCamera` property.
- Bind the `SelectedItem` property of the `Picker` to the `SelectedResolution` property on the `CameraViewModel` class.

The final change involves binding the `ImageCaptureResolution` property of the `CameraView` to the `SelectedResolution` property on the `CameraViewModel` class.

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.CameraViewPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    
    <Grid ColumnDefinitions="*,*,*" RowDefinitions="*,30,30">
        <toolkit:CameraView 
            Grid.ColumnSpan="3" 
            Grid.Row="0"
            SelectedCamera="{Binding SelectedCamera}"
            ZoomFactor="{Binding CurrentZoom}"
            CameraFlashMode="{Binding FlashMode}"
            ImageCaptureResolution="{Binding SelectedResolution}" />

        <Slider 
            Grid.Column="0"
            Grid.Row="1"
            Value="{Binding CurrentZoom}"
            Maximum="{Binding SelectedCamera.MaximumZoomFactor, FallbackValue=1}"
            Minimum="{Binding SelectedCamera.MinimumZoomFactor, FallbackValue=1}"/>

        <Picker 
            Grid.Column="1"
            Grid.Row="1"
            Title="Flash"
            IsVisible="{Binding Path=SelectedCamera.IsFlashSupported, FallbackValue=false}"
            ItemsSource="{Binding FlashModes}"
            SelectedItem="{Binding FlashMode}" />

        <Picker 
            Grid.Column="2"
            Grid.Row="1"
            Title="Available Resolutions"
            ItemsSource="{Binding SelectedCamera.SupportedResolutions}"
            SelectedItem="{Binding SelectedResolution}" />
    </Grid>

</ContentPage>
```

## CaptureImage

The `CameraView` provides the ability to programmatically trigger an image capture. This is possible through both the `CaptureImage` method or the `CaptureImageCommand`.

The following example shows how to add a `Button` into the application and setup the following bindings:

- Bind the `Command` property of the `Button` to the `CaptureImageCommand` property on the `CameraView`.

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.CameraViewPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    
    <Grid ColumnDefinitions="*,*,*" RowDefinitions="*,30,30">
        <toolkit:CameraView
            x:Name="Camera" 
            Grid.ColumnSpan="3" 
            Grid.Row="0"
            SelectedCamera="{Binding SelectedCamera}"
            ZoomFactor="{Binding CurrentZoom}"
            CameraFlashMode="{Binding FlashMode}" />

        <Slider 
            Grid.Column="0"
            Grid.Row="1"
            Value="{Binding CurrentZoom}"
            Maximum="{Binding SelectedCamera.MaximumZoomFactor, FallbackValue=1}"
            Minimum="{Binding SelectedCamera.MinimumZoomFactor, FallbackValue=1}"/>

        <Picker 
            Grid.Column="1"
            Grid.Row="1"
            Title="Flash"
            IsVisible="{Binding Path=SelectedCamera.IsFlashSupported, FallbackValue=false}"
            ItemsSource="{Binding FlashModes}"
            SelectedItem="{Binding FlashMode}" />

        <Picker 
            Grid.Column="2"
            Grid.Row="1"
            Title="Available Resolutions"
            ItemsSource="{Binding SelectedCamera.SupportedResolutions}"
            SelectedItem="{Binding SelectedResolution}" />

        <Button
            Grid.Column="0"
            Grid.Row="2"
            Command="{Binding CaptureImageCommand, Source={x:Reference Camera}}"
            Text="Capture Image" />
    </Grid>

</ContentPage>
```

> [!NOTE]
> In order to use the image that has been captured the `CameraView` provides the `MediaCaptured` event.

> [!NOTE]
> `CaptureImage` ends with the platform's answer to the capture. A failure that a command reports through the `MediaCaptureFailed` event while the capture waits, for example a video recording that `StartVideoRecordingCommand` can't start, doesn't end the capture.

The following example demonstrates how to use the `CaptureImage` method:

> [!NOTE]
> The C# code below uses the Camera field defined above in XAML (`<toolkit:CameraView x:Name="Camera" />`)

```cs
async void HandleCaptureButtonTapped(object? sender, EventArgs e)
{
    try
    {
        // Use the Camera field defined above in XAML (`<toolkit:CameraView x:Name="Camera" />`)
        var captureImageCTS = new CancellationTokenSource(TimeSpan.FromSeconds(3));
        Stream stream = await Camera.CaptureImage(captureImageCTS.Token);
    }
    catch(Exception ex)
    {
        // Handle Exception
        Trace.WriteLine(ex);
    }
}
```


## Video Recording

The `CameraView` provides the ability to record videos. This is possible through both the `StartVideoRecording` method or the `StartVideoRecordingCommand`.

The following example shows how to add a `Button` into the application and setup the following bindings:

- Bind the `Command` property of the `Button` to the `StartVideoRecordingCommand` property on the `CameraView`.

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.CameraViewPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    
    <Grid ColumnDefinitions="*,*,*" RowDefinitions="*,30,30">
        <toolkit:CameraView
            x:Name="Camera" 
            Grid.ColumnSpan="3" 
            Grid.Row="0"
            SelectedCamera="{Binding SelectedCamera}"
            ZoomFactor="{Binding CurrentZoom}"
            CameraFlashMode="{Binding FlashMode}" />

        <Slider 
            Grid.Column="0"
            Grid.Row="1"
            Value="{Binding CurrentZoom}"
            Maximum="{Binding SelectedCamera.MaximumZoomFactor, FallbackValue=1}"
            Minimum="{Binding SelectedCamera.MinimumZoomFactor, FallbackValue=1}"/>

        <Picker 
            Grid.Column="1"
            Grid.Row="1"
            Title="Flash"
            IsVisible="{Binding Path=SelectedCamera.IsFlashSupported, FallbackValue=false}"
            ItemsSource="{Binding FlashModes}"
            SelectedItem="{Binding FlashMode}" />

        <Picker 
            Grid.Column="2"
            Grid.Row="1"
            Title="Available Resolutions"
            ItemsSource="{Binding SelectedCamera.SupportedResolutions}"
            SelectedItem="{Binding SelectedResolution}" />

        <Button Clicked="StartCameraRecording"
                Text="StartVideoRecording" />

        <Button Command="{Binding StartVideoRecordingCommand, Source={x:Reference Camera}, x:DataType=toolkit:CameraView}"
                CommandParameter="{Binding Stream}"
                Text="StartVideoRecording" />

        <Button Command="{Binding StopVideoRecordingCommand, Source={x:Reference Camera}, x:DataType=toolkit:CameraView}"
                CommandParameter="{Binding Token}"
                Text="StopVideoRecording" />
    </Grid>

</ContentPage>
```

> [!NOTE]
> You must provide a clean stream in order to record the video.

The following example demonstrates how to use the `StartVideoRecording` method:

> [!NOTE]
> The C# code below uses the Camera field defined above in XAML (`<toolkit:CameraView x:Name="Camera" />`)

```cs
async void StartCameraRecordingWithCustomStream(object? sender, EventArgs e)
{
    using var threeSecondVideoRecordingStream = new FileStream("recording.mp4", FileMode.Create);
    await Camera.StartVideoRecording(threeSecondVideoRecordingStream, CancellationToken.None);

    await Task.Delay(TimeSpan.FromSeconds(3));
    
    await Camera.StopVideoRecording(CancellationToken.None);
    await FileSaver.SaveAsync("recording.mp4", threeSecondVideoRecordingStream);
}
```

In case you want to record a short video and record video in `MemoryStream` you can use the next overload of VideoRecording:

```cs
async void StartCameraRecording(object? sender, EventArgs e)
{
    await Camera.StartVideoRecording(CancellationToken.None);
    
    await Task.Delay(TimeSpan.FromSeconds(3));
    
    var threeSecondVideoRecordingStream = await Camera.StopVideoRecording(CancellationToken.None);
    await FileSaver.SaveAsync("recording.mp4", threeSecondVideoRecordingStream);
}
```

> [!NOTE]
> `StartVideoRecording` throws a `CameraException` when the recording can't start, for example on iOS and Mac Catalyst when the camera permission isn't granted. It throws an `OperationCanceledException` when its token is cancelled, or `StopCameraPreview` is called, before the recording started. See [Cancel pending starts](#cancel-pending-starts).

## Start preview

The `CameraView` provides the ability to programmatically start the preview from the camera. This is possible through both the `StartCameraPreview` method or the `StartCameraPreviewCommand`.

The following example shows how to add a `Button` into the application and setup the following bindings:

- Bind the `Command` property of the `Button` to the `StartCameraPreviewCommand` property on the `CameraView`.

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.CameraViewPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    
    <Grid ColumnDefinitions="*,*,*" RowDefinitions="*,30,30">
        <toolkit:CameraView
            x:Name="Camera"  
            Grid.ColumnSpan="3" 
            Grid.Row="0"
            SelectedCamera="{Binding SelectedCamera}"
            ZoomFactor="{Binding CurrentZoom}"
            CameraFlashMode="{Binding FlashMode}" />

        <Slider 
            Grid.Column="0"
            Grid.Row="1"
            Value="{Binding CurrentZoom}"
            Maximum="{Binding SelectedCamera.MaximumZoomFactor, FallbackValue=1}"
            Minimum="{Binding SelectedCamera.MinimumZoomFactor, FallbackValue=1}"/>

        <Picker 
            Grid.Column="1"
            Grid.Row="1"
            Title="Flash"
            IsVisible="{Binding Path=SelectedCamera.IsFlashSupported, FallbackValue=false}"
            ItemsSource="{Binding FlashModes}"
            SelectedItem="{Binding FlashMode}" />

        <Picker 
            Grid.Column="2"
            Grid.Row="1"
            Title="Available Resolutions"
            ItemsSource="{Binding SelectedCamera.SupportedResolutions}"
            SelectedItem="{Binding SelectedResolution}" />

        <Button
            Grid.Column="0"
            Grid.Row="2"
            Command="{Binding CaptureImageCommand, Source={x:Reference Camera}}"
            Text="Capture Image" />

        <Button
            Grid.Column="1"
            Grid.Row="2"
            Command="{Binding StartCameraPreviewCommand, Source={x:Reference Camera}}"
            Text="Start Preview" />
    </Grid>

</ContentPage>
```

The following example demonstrates how to use the `StartCameraPreview` method:

> [!NOTE]
> The C# code below uses the Camera field defined above in XAML (`<toolkit:CameraView x:Name="Camera" />`)

```cs
async void HandleStartCameraPreviewButtonTapped(object? sender, EventArgs e)
{

    try
    {
        var startCameraPreviewTCS = new CancellationTokenSource(TimeSpan.FromSeconds(3));

        // Use the Camera field defined above in XAML (`<toolkit:CameraView x:Name="Camera" />`)
        await Camera.StartCameraPreview(startCameraPreviewTCS.Token);
    }
    catch(OperationCanceledException)
    {
        // The token was cancelled, or StopCameraPreview was called, before the preview started
    }
    catch(Exception ex)
    {
        // Handle Exception
        Trace.WriteLine(ex);
    }
}
```

On Android, a `StartCameraPreview` that you call while the `CameraView` is still connecting to its camera waits for the connection, then starts the preview.

A preview that can't start doesn't throw an exception. `StartCameraPreview` and `StartCameraPreviewCommand` report it through the `ErrorOccurred` event on every platform. This includes a device without a camera, a camera permission that isn't granted, and a selected camera that can't be opened, for example because another app is using it. `StartCameraPreview` throws only an `OperationCanceledException` when the start is cancelled, and an `InvalidOperationException` when the `CameraView` has no handler yet, for example before it is shown.

```cs
Camera.ErrorOccurred += (sender, e) => Trace.WriteLine(e.Exception);
```

What happens next depends on why the start failed:

- **The selected camera can't be opened.** The preview stays stopped, but it follows `SelectedCamera`: selecting another camera starts the preview with that camera. This holds until `StopCameraPreview` is called.
- **The camera permission isn't granted.** The preview stays stopped, and selecting another camera doesn't start it. Call `StartCameraPreview` again once the app has the permission. On Android, the preview also starts by itself when the app resumes with the permission granted, for example after the user allowed it in the permission dialog or in the app's settings. This lets a `CameraView` that connects while your app asks for the permission start its preview without another call. A failure of that automatic start is reported through `ErrorOccurred`. Only the last start counts: `StopCameraPreview`, or a later `StartCameraPreview`, cancels it.

## Stop preview

The `CameraView` provides the ability to programmatically stop the preview from the camera. This is possible through both the `StopCameraPreview` method or the `StopCameraPreviewCommand`.

The following example shows how to add a `Button` into the application and setup the following bindings:

- Bind the `Command` property of the `Button` to the `StopCameraPreviewCommand` property on the `CameraView`.

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.CameraViewPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    
    <Grid ColumnDefinitions="*,*,*" RowDefinitions="*,30,30">
        <toolkit:CameraView
            x:Name="Camera"  
            Grid.ColumnSpan="3" 
            Grid.Row="0"
            SelectedCamera="{Binding SelectedCamera}"
            ZoomFactor="{Binding CurrentZoom}"
            CameraFlashMode="{Binding FlashMode}" />

        <Slider 
            Grid.Column="0"
            Grid.Row="1"
            Value="{Binding CurrentZoom}"
            Maximum="{Binding SelectedCamera.MaximumZoomFactor, FallbackValue=1}"
            Minimum="{Binding SelectedCamera.MinimumZoomFactor, FallbackValue=1}"/>

        <Picker 
            Grid.Column="1"
            Grid.Row="1"
            Title="Flash"
            IsVisible="{Binding Path=SelectedCamera.IsFlashSupported, FallbackValue=false}"
            ItemsSource="{Binding FlashModes}"
            SelectedItem="{Binding FlashMode}" />

        <Picker 
            Grid.Column="2"
            Grid.Row="1"
            Title="Available Resolutions"
            ItemsSource="{Binding SelectedCamera.SupportedResolutions}"
            SelectedItem="{Binding SelectedResolution}" />

        <Button
            Grid.Column="0"
            Grid.Row="2"
            Command="{Binding CaptureImageCommand, Source={x:Reference Camera}}"
            Text="Capture Image" />

        <Button
            Grid.Column="1"
            Grid.Row="2"
            Command="{Binding StartCameraPreviewCommand, Source={x:Reference Camera}}"
            Text="Start Preview" />

        <Button
            Grid.Column="2"
            Grid.Row="2"
            Command="{Binding StopCameraPreviewCommand, Source={x:Reference Camera}}"
            Text="Stop Preview" />
    </Grid>

</ContentPage>
```

The following example demonstrates how to use the `StopCameraPreview` method:

> [!NOTE]
> The C# code below uses the Camera field defined above in XAML (`<toolkit:CameraView x:Name="Camera" />`)

```cs
void HandleStopCameraPreviewButtonTapped(object? sender, EventArgs e)
{

    try
    {
        // Use the Camera field defined above in XAML (`<toolkit:CameraView x:Name="Camera" />`)
        Camera.StopCameraPreview();
    }
    catch(Exception ex)
    {
        // Handle Exception
        Trace.WriteLine(ex);
    }
}
```

### Cancel pending starts

`StopCameraPreview` also cancels what is still waiting for the platform to start:

- A `StartCameraPreview` or `StartVideoRecording` (both overloads) that hasn't completed.
- The start that the `CameraView` makes when it connects to its camera.
- A camera switch, which is a change of `SelectedCamera`.
- On Android, the restart of the preview for a new `ImageCaptureResolution`, and the automatic start that waits for the camera permission.

None of these is reported as a failure. The preview stays stopped until you call `StartCameraPreview` again.

A caller that awaits a cancelled `StartCameraPreview` or `StartVideoRecording` gets an `OperationCanceledException`, as when its own token is cancelled. This happens, for example, when the page closes or the user taps a stop button while the camera is still starting. The commands don't report it as an error. On iOS and Mac Catalyst, `StartCameraPreview` with a token that is already cancelled also throws an `OperationCanceledException`, and doesn't start the preview. On Windows, a `StartCameraPreview` that its own token cancels after the camera has opened stops the preview that it had shown, and releases the camera.

> [!IMPORTANT]
> Catch the `OperationCanceledException` when you await these methods, in particular in an `async void` handler, where an exception that escapes ends the app. Call the start again if you still need the preview or the recording after a `StopCameraPreview` interrupted its start.

## Properties

| Property | Type | Description | Default Value |
|---------|---------|---------|---------|
| `CameraFlashMode` | `CameraFlashMode` | Gets or sets the flash mode for the camera. This is a bindable property. | `CameraFlashMode.Off` |
| `ImageCaptureResolution` | `Size` | Gets or sets the resolution for image capture. Does not affect the preview resolution. This is a bindable property. | `Size.Zero` |
| `IsAvailable` | `bool` | Gets whether the camera is available on the device. This is a read-only bindable property. | `false` |
| `IsBusy` | `bool` | Gets whether the camera is currently busy (e.g. capturing an image or recording). This is a read-only bindable property. | `false` |
| `IsTorchOn` | `bool` | Gets or sets whether the camera torch (flashlight) is enabled. This is a bindable property. | `false` |
| `SelectedCamera` | `CameraInfo?` | Gets or sets the currently selected camera device. This is a bindable property with two-way binding. | `null` |
| `ZoomFactor` | `float` | Gets or sets the camera zoom factor. The value is automatically clamped to the selected camera's `MinimumZoomFactor` and `MaximumZoomFactor`. This is a bindable property. | `1f` |

## Commands

| Command | Command Parameter | Description |
|---------|---------|---------|
| `CaptureImageCommand` | `CancellationToken` | Triggers an image capture. The captured image is returned via the `MediaCaptured` event. A capture that fails is reported through the `MediaCaptureFailed` event. |
| `StartCameraPreviewCommand` | `CancellationToken` | Starts the camera preview display. A preview that can't start is reported through the `ErrorOccurred` event. |
| `StartVideoRecordingCommand` | `Stream` | Starts video recording into the `Stream`. A recording that can't start is reported through the `MediaCaptureFailed` event. |
| `StopCameraPreviewCommand` | — | Stops the camera preview display, and cancels a start that is still in progress. A failure is reported through the `ErrorOccurred` event. |
| `StopVideoRecordingCommand` | `CancellationToken` | Stops video recording. The video is written to the `Stream` that was passed to `StartVideoRecordingCommand`. A failure is reported through the `MediaCaptureFailed` event. |

The commands let no exception escape. `ICommand.Execute` can't return the task of the work that a command starts, so an exception would reach no caller and end the app. Each failure is reported once, through the event in the table above. A command whose token is cancelled ends without an event, and so does a start that `StopCameraPreview` cancels.

## Events

| Event | Type | Description |
|---------|---------|---------|
| `MediaCaptured` | `EventHandler<MediaCapturedEventArgs>` | Raised when an image is successfully captured. The `MediaCapturedEventArgs` contains a `Media` property of type `Stream` with the captured image data. |
| `MediaCaptureFailed` | `EventHandler<MediaCaptureFailedEventArgs>` | Raised when an image capture fails, and when `StartVideoRecordingCommand` or `StopVideoRecordingCommand` fails. The `MediaCaptureFailedEventArgs` contains a `FailureReason` property with the error message. |
| `ErrorOccurred` | `EventHandler<ErrorOccurredEventArgs>` | Raised when the camera reports an error that no caller can catch, or a failure that `StartCameraPreview` reports instead of throwing. This covers connecting the camera when the `CameraView` is shown, switching to the camera in `SelectedCamera`, applying `ImageCaptureResolution`, a preview that can't start, the automatic start on Android once the camera permission is granted and, on Windows, updating `IsAvailable`. The `ErrorOccurredEventArgs` contains an `Exception` property with the exception. A start that `StopCameraPreview` cancels isn't an error and isn't reported. |

## Methods

| Method | Return Type | Description |
|---------|---------|---------|
| `CaptureImage(CancellationToken)` | `Task<Stream>` | Captures a single image from the camera and returns it. The image is also delivered via the `MediaCaptured` event. Throws a `CameraException` when the capture fails, for example when the preview hasn't started, and raises the `MediaCaptureFailed` event with the same reason. |
| `GetAvailableCameras(CancellationToken)` | `ValueTask<IReadOnlyList<CameraInfo>>` | Retrieves a list of available camera devices on the device. |
| `StartCameraPreview(CancellationToken)` | `Task` | Starts displaying the camera preview. A preview that can't start is reported through the `ErrorOccurred` event. Throws an `OperationCanceledException` when the token is cancelled, or `StopCameraPreview` is called, before the preview started. |
| `StartVideoRecording(CancellationToken)` | `Task` | Starts recording video to an internal `MemoryStream`. Throws an `OperationCanceledException` when the token is cancelled, or `StopCameraPreview` is called, before the recording started. |
| `StartVideoRecording(Stream, CancellationToken)` | `Task` | Starts recording video to the provided `Stream`. Throws an `OperationCanceledException` when the token is cancelled, or `StopCameraPreview` is called, before the recording started. |
| `StopCameraPreview()` | `void` | Stops displaying the camera preview, and cancels a start of the preview or of a recording that is still in progress. |
| `StopVideoRecording(CancellationToken)` | `Task<Stream>` | Stops video recording and returns the recorded `Stream`. |

## CameraInfo

The `CameraInfo` class represents information about a camera device available on the system.

| Property | Type | Description |
|---------|---------|---------|
| `DeviceId` | `string` | The unique identifier of the camera device. |
| `IsFlashSupported` | `bool` | Whether the camera supports flash. |
| `MaximumZoomFactor` | `float` | The maximum supported zoom factor. |
| `MinimumZoomFactor` | `float` | The minimum supported zoom factor. |
| `Name` | `string` | The name of the camera device. |
| `Position` | `CameraPosition` | The physical position of the camera on the device (`Front`, `Rear`, or `Unknown`). |
| `SupportedResolutions` | `IReadOnlyList<Size>` | The list of resolutions supported by the camera for image capture. |

## CameraFlashMode

The `CameraFlashMode` enum defines the available flash modes.

| Value | Description |
|---------|---------|
| `Off` | The flash is off and will not be used. |
| `On` | The flash is on and will always be used. |
| `Auto` | The flash will automatically be used based on the lighting conditions. |

## CameraPosition

The `CameraPosition` enum defines the possible physical positions of a camera on a device.

| Value | Description |
|---------|---------|
| `Unknown` | The camera position is unknown. |
| `Front` | The camera is at the front of the device (facing the user). |
| `Rear` | The camera is at the rear of the device (facing away from the user). |

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/CameraView/CameraViewPage.xaml.cs).

## API

You can find the source code for `CameraView` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Camera/Views/CameraView.shared.cs).
