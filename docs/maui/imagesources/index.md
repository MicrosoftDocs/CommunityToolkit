---
title: ImageSources - .NET MAUI Community Toolkit
author: GeorgeLeithead
description: The .NET MAUI Community Toolkit extends .NET MAUI ImageSources.
ms.date: 08/18/2022
---

# ImageSources

The user interface of a .NET Multi-platform App UI (.NET MAUI) app is constructed of objects that map to the native controls of each target platform.

The main control groups used to create the user interface of a .NET MAUI app are pages, layouts, and views. A .NET MAUI page generally occupies the full screen or window. The page usually contains a layout, which contains views and possibly other layouts. Pages, layouts, and views derive from the `VisualElement` class. This class provides a variety of properties, methods, and events that are useful in derived classes.

For further information on Behaviors please refer to the [.NET MAUI documentation](/dotnet/maui/user-interface/controls/).

The .NET Multi-platform App UI (.NET MAUI) Image displays an `image` that can be loaded from a local file, a URI, an embedded resource, or a stream. The standard platform image formats are supported, including animated GIFs, and local Scalable Vector Graphics (SVG) files are also supported.  For more information about the `Image` control, see [Image](/dotnet/maui/user-interface/controls/image).

`Images` define a `Source` property, of type `ImageSource`, which specifies the source of the image.  The `ImageSource` class defines the following methods that can be used to load an image from different sources:

- `FromFile` returns a `FileImageSource` that reads an image from a local file.
- `FromUri` returns an `UriImageSource` that downloads and reads an image from a specified URI.
- `FromResource` returns a `StreamImageSource` that reads an image file embedded in an assembly.
- `FromStream` returns a `StreamImageSource` that reads an image from a stream that supplies image data.

## .NET MAUI Community Toolkit ImageSources

The .NET MAUI Community Toolkit provides a collection of additional pre-built, reusable `ImageSources` to make developers lives easier. Here are the sources provided by the toolkit:

| View | Description |
| --------- | ----------- |
| [`GravatarImageSource`](GravatarImageSource.md) | The `GravatarImageSource` provides an Image source to display a users Gravatar registered image via their email address. |