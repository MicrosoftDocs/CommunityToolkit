---
title: Animations - .NET MAUI Community Toolkit
author: bijington
description: The .NET MAUI Community Toolkit provides a collection of pre-built, reusable animations to make developers lives easier.
ms.date: 09/16/2022
---

# Animations

The .NET Multi-platform App UI (.NET MAUI) animation classes target different properties of visual elements, with a typical basic animation progressively changing a property from one value to another over a period of time.

For further information on Animations please refer to the [.NET MAUI documentation](/dotnet/maui/user-interface/animation/basic).

## .NET MAUI Community Toolkit Animations

The .NET MAUI Community Toolkit provides a collection of pre-built, reusable animations that can be used in both C# and XAML. Here are the animations provided by the toolkit:

| Behavior | Description |
| --------- | ----------- |
| [`FadeAnimation`](../animations/fade-animation.md) | The `FadeAnimation` provides the ability to animate the opacity of a `VisualElement` from it's original opacity, to a specified new opacity and then back to the original. |

## Creating custom animations

All animations provided by the .NET MAUI Community Toolkit inherit from our `BaseAnimation` class. In order to create any custom animation of your choosing you can do the same.

The following example shows how to change the `BackgroundColor` of a `VisualElement` using our very own [`BackgroundColorTo`](../extensions/color-animation-extensions.md#backgroundcolorto) extension method.

```csharp
using CommunityToolkit.Maui.Extensions;

class PaintTheRainbowAnimation : BaseAnimation
{
    public override Task Animate(VisualElement view)
    {
        await view.BackgroundColorTo(Colors.Red);
        await view.BackgroundColorTo(Colors.Orange);
        await view.BackgroundColorTo(Colors.Yellow);
        await view.BackgroundColorTo(Colors.Green);
        await view.BackgroundColorTo(Colors.Blue);
        await view.BackgroundColorTo(Colors.Indigo);
        await view.BackgroundColorTo(Colors.Violet);
    }
}
```
