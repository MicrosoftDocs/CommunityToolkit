---
title: Map - .NET MAUI Community Toolkit
author: jfversluis
description: "The Map control is a cross-platform view for displaying and annotating maps. The Windows implementation is available through the .NET MAUI Community Toolkit."
ms.date: 10/23/2026
---

# Map

The `Map` control is a cross-platform view for displaying and annotating maps. The Windows implementation is available through the .NET MAUI Community Toolkit.

> [!IMPORTANT]
> Bing Maps has stopped giving out new API keys that are needed for this control to work. We are currently deciding if we should update this control to use the WinUI control that uses Azure Maps or that we will wait for the official .NET MAUI first-party implementation for this.
> For the time being that means you cannot use this control if you do not already have a Bing Maps API key. Bing Maps as a whole will be discontinued entirely on June 30th, 2025.

## Setup

Before you are able to use `Map` inside your application you will need to install the NuGet package and add an initialization line in your *MauiProgram.cs*. For more information on how to do this, please refer to the [Get Started](../get-started.md) page.

## Usage

The API of the .NET MAUI Community Toolkit implementation for Windows is not different from the API of the .NET MAUI Maps implementation for iOS and Android.

For details on how to work with this map control, please refer to the [.NET MAUI Map documentation](/dotnet/maui/user-interface/controls/map).

## Map types

The `MapType` of the map decides what the Windows map shows, as it does on iOS and Android:

|MapType  |Windows shows  |
|---------|---------|
| `Street` | The road map. |
| `Satellite` | Aerial imagery without place or road labels. |
| `Hybrid` | Aerial imagery with labels. |

A value outside of the `MapType` enumeration shows the road map.

> [!NOTE]
> Earlier versions showed the labels for `Satellite` too, so it looked the same as `Hybrid`. If your app chose `Satellite` on Windows to get labels, choose `Hybrid`.

## Examples

You can find examples of this control in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/tree/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/Maps).

## API

You can find the source code for `Map` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Maps/AppHostBuilderExtensions.shared.cs).
