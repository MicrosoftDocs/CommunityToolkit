---
title: Map - .NET MAUI Community Toolkit
author: jfversluis
description: "The Map control is a cross-platform view for displaying and annotating maps. The .NET MAUI Community Toolkit provides a Windows implementation that uses Bing Maps."
ms.date: 11/05/2026
---

# Map

The `Map` control is a cross-platform view for displaying and annotating maps. The .NET MAUI Community Toolkit provides a Windows implementation that uses Bing Maps.

> [!WARNING]
> `CommunityToolkit.Maui.Maps` is deprecated and will be removed in a future release. Use .NET MAUI's own `Map` from the `Microsoft.Maui.Controls.Maps` package, which supports Windows starting with .NET MAUI 10. On Windows, it uses the WinUI 3 `MapControl`, which is backed by Azure Maps.
>
> To move to it, remove the `CommunityToolkit.Maui.Maps` package and make sure your project references the `Microsoft.Maui.Controls.Maps` package directly, because `CommunityToolkit.Maui.Maps` referenced it for you. Remove `using CommunityToolkit.Maui.Maps;` and the call to `UseMauiCommunityToolkitMaps`, and call `UseMauiMaps` on every platform. On Windows, set your Azure Maps subscription key with `builder.ConfigureEssentials(essentials => essentials.UseMapServiceToken("YOUR_AZURE_MAPS_SUBSCRIPTION_KEY"))`. Without a valid key, the map shows no map data. For more information, see [Map](/dotnet/maui/user-interface/controls/map).
>
> On Windows, the .NET MAUI `Map` doesn't support:
>
> - `IsShowingUser`
> - Polygons, polylines and circles in `MapElements`
> - Pin labels and info windows
> - The `MapClicked` event
>
> It supports `MoveToRegion`, the `Street`, `Satellite` and `Hybrid` map types, traffic, scrolling, zooming and pins.
>
> This library implements `Map` on Windows with Bing Maps for Enterprise, which Microsoft is retiring: free (Basic) accounts were retired on June 30, 2025, and Enterprise accounts can use it until June 30, 2028. For more information, see [Deprecate Map Control in favor of MAUI Map implementation](https://github.com/CommunityToolkit/Maui/issues/3190).

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
