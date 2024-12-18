---
title: Views - .NET MAUI Community Toolkit
author: jfversluis
description: The .NET MAUI Community Toolkit extends .NET MAUI controls.
ms.date: 06/13/2023
---

# Views

The user interface of a .NET Multi-platform App UI (.NET MAUI) app is constructed of objects that map to the native controls of each target platform.

The main control groups used to create the user interface of a .NET MAUI app are pages, layouts, and views. A .NET MAUI page generally occupies the full screen or window. The page usually contains a layout, which contains views and possibly other layouts. Pages, layouts, and views derive from the `VisualElement` class. This class provides a variety of properties, methods, and events that are useful in derived classes.

For further information on Behaviors please refer to the [.NET MAUI documentation](/dotnet/maui/user-interface/controls/).

## .NET MAUI Community Toolkit Views

The .NET MAUI Community Toolkit provides a collection of pre-built, reusable views to make developers lives easier. Here are the behaviors provided by the toolkit:

| View | Description |
| --------- | ----------- |
| [`AvatarView`](AvatarView.md) | The `AvatarView` is a control for displaying a user's avatar image or their initials. |
| [`CameraView`](camera-view.md) | The `CameraView` provides the ability to connect to a camera, display a preview from the camera and take photos. |
| [`DrawingView`](DrawingView.md) | The `DrawingView` provides a surface that allows for the drawing of lines through the use of touch or mouse interaction. The result of a users drawing can be saved out as an image. |
| [`Expander`](Expander.md) | The `Expander` control provides an expandable container to host any content. |
| [`LazyView`](LazyView.md) | The `LazyView` control allows you to delay the initialization of a View.|
| [`Map (Windows)`](Map.md) | The `Map` control is a cross-platform view for displaying and annotating maps. The Windows implementation is available through the .NET MAUI Community Toolkit. |
| [`MediaElement`](MediaElement.md) | The `MediaElement` is a view for playing multimedia such as audio and video. |
| [`Popup`](Popup.md) | The `Popup` view allows developers to build their own custom UI and present it to their users. |
| [`SemanticOrderView`](semantic-order-view.md) | The `SemanticOrderView` provides the ability to control the order of VisualElements for screen readers and improve the Accessibility of an application. |
