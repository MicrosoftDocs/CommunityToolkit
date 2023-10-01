---
title: .NET MAUI Community Toolkit - Markup
author: brminnick
description: C# Markup supports C# Hot Reload
ms.date: 10/01/2023
---

# C# Markup Hot Reload

## Basic Usage

To use [.NET Hot Reload](https://devblogs.microsoft.com/dotnet/introducing-net-hot-reload/), whilst actively debugging your .NET MAUI app, modify its C# code, then click the **Apply Code Changes** button (aka the 🔥 button) in the Visual Studio toolbar.

![C# Hot Reload Demo](dotnet-hot-reload.gif)

> [!WARNING]
> When modifying UI code, the **Apply Code Changes** button (aka the 🔥 button) will update the running C# code immediately, but it may not update your UI immediately (see [Advanced Usage](./dotnet-hot-reload.md#advanced-usage)). This is because .NET MAUI is not aware of the underlying changes you've just made to the runnning [Intermediate Language](https://learn.microsoft.com/dotnet/standard/managed-code#intermediate-language--execution). 
> 
> The good news is the running code has indeed been updated, and we just need to tell .NET MAUI to redraw the updated UI onto the screen
>
> An easy solution is to force .NET MAUI to update its UI by navigating away from the current page where the .NET Hot Reload change was applied, and then navigating back to that page. This forces .NET MAUI to redraw the UI on the screen.
>
> See [Advanced Usage](./dotnet-hot-reload.md#advanced-usage) for more information on how to automatically tell .NET MAUI to redraw the updated UI.

## Advanced Usage

There exists a gap in the .NET ecosystem between .NET MAUI and .NET Hot Reload: your .NET MAUI app UI does not automatically refresh after pressing the **Apply Code Changes** button (aka the 🔥 button). Whilst your code has been updated in the app's underlying [Intermediate Language](https://learn.microsoft.com/dotnet/standard/managed-code#intermediate-language--execution), nothing has told .NET MAUI to redraw the updated UI on the screen.

The good news is that we can manually tell .NET MAUI to redraw the UI by implementing `ICommunityToolkitHotReloadHandler` and registering it with .NET MAUI's Dependency Injection container ([example below](./dotnet-hot-reload.md#example-icommunitytoolkithotreloadhandler-implementation)).

### MetadataUpdateHandler 
When [.NET Hot Reload](https://devblogs.microsoft.com/dotnet/introducing-net-hot-reload/) executes, it surfaces each updated `Type` by providing a `Type[]` via [`System.Reflection.Metadata.MetadataUpdateHandler`](https://learn.microsoft.com/dotnet/api/system.reflection.metadata.metadataupdatehandlerattribute). 

The .NET MAUI C# Markup Community Toolkit surfaces the changed types via `ICommunityToolkitHotReloadHandler.OnHotReload(IReadOnlyList<Type> types)`. 

Registering your implementation of `ICommunityToolkitHotReloadHandler` with .NET MAUI's Dependency Injection container ensures the `OnHotReload` method will automatically fire each time the **Apply Code Changes** button (aka the 🔥 button) is pressed: 

```cs
builder.Services.AddSingleton<ICommunityToolkitHotReloadHandler, HotReloadHandler>();
```

### Example Implementation of `ICommunityToolkitHotReloadHandler`

This example demonstrates how to implement `ICommunityToolkitHotReloadHandler` to tell .NET MAUI to automatically redraw your app UI when the **Apply Code Changes** button (aka the 🔥 button) is pressed. 

> [!NOTE]
> This is not a comprehensive example that will work for every app. This example will work for most apps, but because every .NET MAUI app is architected + implemented differently, we recommend modifying the example code to best work for your code base.

#### MauiProgram.cs

In **MauiProgram.cs**, add your implementation of `ICommunityToolkitHotReloadHandler` to .NET MAUI's Dependency Injection container:

```cs
public class MauiProgram
{
	public static MauiApp CreateMauiApp()
	{
		// ...
        // Additional code ommitted for brevity
        // ...

		// Register C# Hot Reload Handler
		builder.Services.AddSingleton<ICommunityToolkitHotReloadHandler, HotReloadHandler>();

		// ...
        // Additional code ommitted for brevity
        // ...
	}
}
```

#### HotReloadHandler.cs

In the implementation of `ICommunityToolkitHotReloadHandler`, we tell .NET MAUI to redraw the UI on the screen.

The below example handles both Shell and non-Shell architectures and includes support for pages displayed modally.

> [!NOTE]
> This is not a comprehensive example that will work for every app. This example will work for most apps, but because every .NET MAUI app is architected + implemented differently, we recommend modifying the example code to best work for your code base.

```cs
using System.Diagnostics;
using System.Diagnostics.CodeAnalysis;

namespace CommunityToolkit.Maui.Markup.Sample;

class HotReloadHandler : ICommunityToolkitHotReloadHandler
{
	public async void OnHotReload(IReadOnlyList<Type> types)
	{
		if (Application.Current?.Windows is null)
		{
			Trace.WriteLine($"{nameof(HotReloadHandler)} Failed: {nameof(Application)}.{nameof(Application.Current)}.{nameof(Application.Current.Windows)} is null");
			return;
		}

		foreach (var window in Application.Current.Windows)
		{
			if (window.Page is not Page currentPage)
			{
				return;
			}

			foreach (var type in types)
			{
				if (type.IsSubclassOf(typeof(Page)))
				{
					if (window.Page is AppShell shell)
					{
						if (shell.CurrentPage is Page visiblePage
							&& visiblePage.GetType() == type)
						{
							var currentPageShellRoute = AppShell.GetRoute(type);

							await currentPage.Dispatcher.DispatchAsync(async () =>
							{
								await shell.GoToAsync(currentPageShellRoute, false);
								shell.Navigation.RemovePage(visiblePage);
							});

							break;
						}
					}
					else
					{
						if (TryGetModalStackPage(window, out var modalPage))
						{
							await currentPage.Dispatcher.DispatchAsync(async () =>
							{
								await currentPage.Navigation.PopModalAsync(false);
								await currentPage.Navigation.PushModalAsync(modalPage, false);
							});
						}
						else
						{
							await currentPage.Dispatcher.DispatchAsync(async () =>
							{
								await currentPage.Navigation.PopAsync(false);
								await currentPage.Navigation.PushAsync(modalPage, false);
							});
						}

						break;
					}
				}
			}
		}
	}


	static bool TryGetModalStackPage(Window window, [NotNullWhen(true)] out Page? page)
	{
		page = window.Navigation.ModalStack.LastOrDefault();
		return page is not null;
	}
}
```