---
title: CameraView - .NET MAUI Community Toolkit
author: bijington
description: "The CameraView provides the ability to connect to a connected camera, display a preview from the camera and take photos."
ms.date: 05/23/2024
---

# CameraView

The `CameraView` provides the ability to connect to a connected camera, display a preview from the camera and take photos. The `CameraView` also offers the options you would expect to support taking photos and recording videos such as turning the flash on or off, saving the captured media to a file, and offering different hooks for events.

The following sections will incrementally build on how to use the `CameraView` in a .NET MAUI application. They rely on the use of a [`CameraViewModel`](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/ViewModels/Views/CameraViewModel.cs). that will be set as the `BindingContext` of the example [`CameraViewPage`](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/CameraViewPage.xaml).

## Platform specific initialization

To first use the `CameraView` please refer to the [Getting started](../get-started.md) section. The following platform specific setup is required.

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

The `CameraView` can be added to a a .NET MAUI application in the following way.

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

## Stop preview

The `CameraView` provides the ability to programmatically start the preview from the camera. This is possible through both the `StopCameraPreview` method or the `StopCameraPreviewCommand`.

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

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/CameraViewPage.xaml.cs).

## API

You can find the source code for `CameraView` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.CameraView/Views/CameraView.shared.cs).
