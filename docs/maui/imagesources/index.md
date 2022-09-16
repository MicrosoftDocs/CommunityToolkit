---
title: ImageSources - .NET MAUI Community Toolkit
author: GeorgeLeithead
description: The .NET MAUI Community Toolkit extends .NET MAUI ImageSources.
ms.date: 09/16/2022
---

# ImageSources

The .NET Multi-platform App UI (.NET MAUI) `Image` displays an image that can be loaded from a local file, a URI, an embedded resource, or a stream. The standard platform image formats are supported, including animated GIFs, and local Scalable Vector Graphics (SVG) files are also supported.  For more information about the `Image` control, see [Image](/dotnet/maui/user-interface/controls/image).

Any control that has a property of type `ImageSource`, can specify the source of an image.  The `ImageSource` property has the following methods that can be used to load an image from different sources:

- `FromFile` returns a `FileImageSource` that reads an image from a local file.
- `FromUri` returns an `UriImageSource` that downloads and reads an image from a specified URI.
- `FromResource` returns a `StreamImageSource` that reads an image file embedded in an assembly.
- `FromStream` returns a `StreamImageSource` that reads an image from a stream that supplies image data.

## .NET MAUI Community Toolkit ImageSources

The .NET MAUI Community Toolkit provides a collection of additional pre-built, reusable `ImageSources` to make developers lives easier. Here are the sources provided by the toolkit:

| View | Description |
| --------- | ----------- |
| [`GravatarImageSource`](GravatarImageSource.md) | The `GravatarImageSource` provides an Image source to display a users Gravatar registered image via their email address. |