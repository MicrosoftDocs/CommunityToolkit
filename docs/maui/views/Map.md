---
title: Map (Removed) - .NET MAUI Community Toolkit
author: jfversluis
description: "CommunityToolkit.Maui.Maps was removed in the .NET 11 release. Use the Map control from Microsoft.Maui.Controls.Maps instead."
ms.date: 11/10/2026
---

# Map (Removed)

> [!WARNING]
> `CommunityToolkit.Maui.Maps` was deprecated in the toolkit's last .NET 10 release and is removed in the .NET 11 release. The package has no .NET 11 version. The `Map` control for Windows that it provided used Bing Maps for Enterprise, which Microsoft is retiring. For more information, see [Deprecate Map Control in favor of MAUI Map implementation](https://github.com/CommunityToolkit/Maui/issues/3190).

.NET MAUI includes its own `Map` control in the `Microsoft.Maui.Controls.Maps` package. It supports Android, iOS, Mac Catalyst, and Windows. On Windows, it uses the WinUI 3 `MapControl`, which is backed by Azure Maps. For details on how to work with the control, see the [.NET MAUI Map documentation](/dotnet/maui/user-interface/controls/map).

## Migrate to the .NET MAUI Map

1. Remove the `CommunityToolkit.Maui.Maps` package from your project.
1. Add the `Microsoft.Maui.Controls.Maps` package to your project. `CommunityToolkit.Maui.Maps` referenced it for you, so your project might not reference it directly yet.
1. Remove `using CommunityToolkit.Maui.Maps;` and the call to `UseMauiCommunityToolkitMaps` from *MauiProgram.cs*.
1. Call `UseMauiMaps` on the `MauiAppBuilder` for every platform.
1. On Windows, set your Azure Maps subscription key. Without a valid key, the map shows no map data.

```csharp
var builder = MauiApp.CreateBuilder();
builder
    .UseMauiApp<App>()
    .UseMauiMaps();

#if WINDOWS
builder.ConfigureEssentials(essentials => essentials.UseMapServiceToken("YOUR_AZURE_MAPS_SUBSCRIPTION_KEY"));
#endif
```

## Windows limitations

On Windows, the .NET MAUI `Map` doesn't support:

- `IsShowingUser`
- Polygons, polylines and circles in `MapElements`
- Pin labels and info windows
- The `MapClicked` event

It supports `MoveToRegion`, the `Street`, `Satellite` and `Hybrid` map types, traffic, scrolling, zooming and pins.
