---
title: CameraView - .NET MAUI Community Toolkit
author: bijington
description: "The CameraView provides the ability to connect to a camera, display a preview from the camera and take photos."
ms.date: 05/23/2024
---

# CameraView

The `CameraView` provides the ability to connect to a camera, display a preview from the camera and take photos. The `CameraView` also offers features to support taking photos, controlling the flash, saving captured media to a file, and offering different hooks for events.

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

This should be added inside the `<manifest>` element. Below shows a more complete example:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    <application android:allowBackup="true" android:icon="@mipmap/appicon" android:roundIcon="@mipmap/appicon_round" android:supportsRtl="true" />

    <uses-permission android:name="android.permission.CAMERA" />

</manifest>
```

### [iOS](#tab/ios)

The following entries need to be added to the `Platforms/iOS/Info.plist` file:

```xml
<key>NSCameraUsageDescription</key>
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
</dict>
</plist>
```

### [Mac Catalyst](#tab/mac)

The following entries need to be added to the `Platforms/MacCatalyst/Info.plist` file:

```xml
<key>NSCameraUsageDescription</key>
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
</dict>
</plist>
```

### [Windows](#tab/windows)

No setup is required.

### [Tizen](#tab/tizen)

Tizen is not currently supported.

-----
<!-- markdownlint-enable MD051 -->
<!-- markdownlint-enable MD025 -->

## Basic usage

The `CameraView` can be added to a .NET MAUI application in the following way.

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

## ICameraProvider

The `ICameraProvider` interface provides access to the list of cameras available on the current device, as well as methods for initializing and refreshing that list. It is registered internally as a singleton service when the `CommunityToolkit.Maui.Camera` package is used (see [Getting started](../get-started.md?tabs=CommunityToolkitMauiCamera)), so it can be injected into view models or other classes through the constructor.

The following example show how to request an `ICameraProvider` through dependency injection and call `InitializeAsync` to obtain a list of available cameras. This performs a one-time discovery of cameras and populates the `AvailableCameras` property. Subsequent calls will reuse the cached results.

```cs
public class CameraViewViewModel(ICameraProvider cameraProvider) 
{
    readonly ICameraProvider cameraProvider = cameraProvider;

    public ObservableCollection<CameraInfo> Cameras { get; } = [];

    public async Task InitializeAsync()
    {
        await cameraProvider.InitializeAsync(CancellationToken.None);
        foreach (var camera in cameraProvider.AvailableCameras ?? [])
        {
            Cameras.Add(camera);
        }
    }
}
```

If camera availability changes at runtime (e.g. an external USB camera is plugged in), call `RefreshAvailableCameras` to force a refresh. Unlike `InitializeAsync`, this always re-runs camera discovery to ensure the list is up to date, at the cost of performance as it may be expensive on some platforms (e.g., Windows).

```cs
await cameraProvider.RefreshAvailableCameras(CancellationToken.None);
Cameras.Clear();
foreach (var camera in cameraProvider.AvailableCameras ?? [])
{
    Cameras.Add(camera);
}
```

## Access and switch the current camera

The `SelectedCamera` property provides the ability to get and set the currently selected camera. 

It is a bindable property with default `TwoWay` binding. This means that when it is bound to a property in a view model, updating the `SelectedCamera` of the `CameraView` will also automatically update the corresponding property in the view model.

The following example shows how to bind the `SelectedCamera` property from the `CameraView` to a property on the `CameraViewModel` with the same name (`SelectedCamera`), and a `Picker` to change the selected camera.

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

        <Picker 
            Grid.Row="1"
            Title="Cameras" 
            ItemsSource="{Binding Cameras}"
            ItemDisplayBinding="{Binding Name}" 
            SelectedItem="{Binding SelectedCamera}" />
    </Grid>

</ContentPage>
```

```cs
public class CameraViewViewModel(ICameraProvider cameraProvider) 
{
    readonly ICameraProvider cameraProvider = cameraProvider;

    public ObservableCollection<CameraInfo> Cameras { get; } = [];

	[ObservableProperty]
	public partial CameraInfo? SelectedCamera { get; set; }

    public async Task InitializeAsync()
    {
        await cameraProvider.InitializeAsync(CancellationToken.None);
        foreach (var camera in cameraProvider.AvailableCameras ?? [])
        {
            Cameras.Add(camera);
        }
        // Optionally set an initial camera
        SelectedCamera = Cameras.LastOrDefault();
    }
}
```

The following describes the different behaviors of the code:

- No initial camera specified
If `SelectedCamera` is not assigned in the view model, the `CameraView` automatically defaults to the first available camera after loading.
Because the binding is `TwoWay`, the `Picker` will also reflect that camera as selected.

- Initial camera specified in the view model
If you assign an initial value (e.g. `SelectedCamera = Cameras.LastOrDefault();`), then both the `CameraView` and the `Picker` will start with that camera selected.

- User changes selection
When the user selects a camera from the `Picker`, the `SelectedCamera` property in the view model is updated, which in turn updates the `CameraView` to display the newly selected camera.

> [!NOTE]
> If the `SelectedCamera` is not specified an initial value, it will be set automatically to the first available camera on the device after the `CameraView` is loaded.

## Control Zoom

The `SelectedCamera` property provides both a `MinimumZoomFactor` and a `MaximumZoomFactor` property, these are read-only and provide developers with a programmatic way of determining what zoom can be applied to the current camera. In order to change the zoom on the current camera the `CameraView` provides the `ZoomFactor` property.

> [!NOTE]
> If a value is provided outside of the `MinimumZoomFactor` and `MaximumZoomFactor` the `CameraView` will clamp the value to keep it within the bounds.

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
    catch(Exception e)
    {
        // Handle Exception
        Trace.WriteLine(e);
    }
}
```

## Start preview

The `CameraView` provides the ability to programmatically start the preview from the camera. This is possible through both the `StartCameraPreview` method or the `StartCameraPreviewCommand`.

> [!NOTE]
> The camera previw is always automatically started when the `CameraView` is loaded, so you don't need to call `StartCameraPreview` explicitly. The `StartCameraPreview` and `StopCameraPreview` is used to stop and start the camera preview after the `CameraView` is loaded and still active.

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
            Text="Capture Image" />
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
    catch(Exception e)
    {
        // Handle Exception
        Trace.WriteLine(e);
    }
}
```

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
            Text="Capture Image" />

        <Button
            Grid.Column="2"
            Grid.Row="2"
            Command="{Binding StopCameraPreviewCommand, Source={x:Reference Camera}}"
            Text="Capture Image" />
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
    catch(Exception e)
    {
        // Handle Exception
        Trace.WriteLine(e);
    }
}
```

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/CameraView/CameraViewPage.xaml.cs).

## API

You can find the source code for `CameraView` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Camera/Views/CameraView.shared.cs).
