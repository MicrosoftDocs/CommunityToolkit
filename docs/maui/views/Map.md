---
title: Map - .NET MAUI Community Toolkit
author: jfversluis
description: "The Map control is a cross-platform view for displaying and annotating maps. The .NET MAUI Community Toolkit provides a Windows implementation that uses Bing Maps."
ms.date: 11/05/2026
---

# Map

The `Map` control is a cross-platform view for displaying and annotating maps. The .NET MAUI Community Toolkit provides a Windows implementation that uses Bing Maps.

> [!WARNING]
> `CommunityToolkit.Maui.Maps` is deprecated and will be removed in a future release. It implements `Map` on Windows with Bing Maps for Enterprise, which Microsoft is retiring: free (Basic) accounts were retired on June 30, 2025, and Enterprise accounts can use it until June 30, 2028. Bing Maps no longer issues new API keys, so you can't use this control on Windows without an existing key.
>
> Starting with .NET MAUI 10.0.70, the .NET MAUI `Map` supports Windows with Azure Maps. To move to it, remove the call to `UseMauiCommunityToolkitMaps`, call `UseMauiMaps` on every platform, and set your Azure Maps key with `UseMapServiceToken`. For more information, see [Map](/dotnet/maui/user-interface/controls/map) and [Deprecate Map Control in favor of MAUI Map implementation](https://github.com/CommunityToolkit/Maui/issues/3190).

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

You can find the source code for `Map` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Maps/AppBuilderExtensions.shared.cs).
