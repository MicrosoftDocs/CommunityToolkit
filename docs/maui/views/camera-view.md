---
title: CameraView - .NET MAUI Community Toolkit
author: bijington
description: "The CameraView provides the ability to connect to a connected camera, display a preview from the camera and take photos."
ms.date: 05/23/2024
---

# CameraView

The `CameraView` provides the ability to connect to a connected camera, display a preview from the camera and take photos. The `CameraView` also offers the options you would expect to support taking photos and recording videos such as turning the flash on or off, saving the captured media to a file, and offering different hooks for events.

The following sections will incrementally build on how to use the `CameraView` in a .NET MAUI application.

## Basic usage

To first use the `CameraView` please refer to the [Getting started](../get-started.md) section.

### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.MyPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    
    <toolkit:CameraView />

</ContentPage>
```

## Control Zoom

The `CameraView` provides both a `MinimumZoomFactor` and a `MaximumZoomFactor` property, these are read-only and provide developers with a programmatic way of determining what zoom can be applied to the current camera. In order to change the zoom on the current camera the `CameraView` provides the `ZoomFactor` property.

> [!NOTE]
> If a value is provided outside of the `MinimumZoomFactor` and `MaximumZoomFactor` the `CameraView` will clamp the value to keep it within the bounds.

## Camera Flash Mode

## ImageCaptureResolution

## Change camera

## CaptureImage

## Start / stop preview
