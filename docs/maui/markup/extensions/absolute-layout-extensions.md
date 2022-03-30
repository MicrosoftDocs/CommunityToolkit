---
title: AbsoluteLayout extensions - .NET MAUI Community Toolkit
author: bijington
description: The AbsoluteLayout extensions provide a series of extension methods that support positioning Views in AbsoluteLayouts.
ms.date: 03/21/2022
---

# AbsoluteLayout extensions

The AbsoluteLayout extensions provide a series of extension methods that support positioning `View`s in `AbsoluteLayout`s.

The extensions offer the following methods:

## LayoutBounds

The `LayoutBounds` extension method allows you to set the position and size of a `View` in an `AbsoluteLayout`. For further detail refer to the [Microsoft documentation](/dotnet/maui/user-interface/layouts/absolutelayout#position-and-size-children).

## LayoutFlags

The `LayoutFlags` extension method allows you to set a flag that indicates that the layout bounds position and size values for a child are proportional to the size of the `AbsoluteLayout`. For further detail refer to the [Microsoft documentation](/dotnet/maui/user-interface/layouts/absolutelayout#proportional-positioning-and-sizing).

## Syntax

Note that both of the methods `LayoutBounds` and `LayoutFlags` can be used in combination to determine whether the position and size of the `View` is are absolute or proportional.

```csharp
using CommunityToolkit.Maui.Markup;
using Microsoft.Maui.Layouts;

public class AbsoluteLayoutSamplePage : ContentPage
{
    public AbsoluteLayoutSamplePage()
    {
        Content = new AbsoluteLayout
        {
            Children =
            {
                new BoxView
                {
                    Color = Colors.Blue,
                }.LayoutFlags(AbsoluteLayoutFlags.PositionProportional)
                .LayoutBounds(0.5, 0, 100, 25),

                new BoxView
                {
                    Color = Colors.Green,
                    WidthRequest = 25,
                    HeightRequest = 100,
                }.LayoutFlags(AbsoluteLayoutFlags.PositionProportional)
                .LayoutBounds(0, 0.5),

                new BoxView
                {
                    Color = Colors.Red,
                    WidthRequest = 25,
                    HeightRequest = 100,
                }.LayoutFlags(AbsoluteLayoutFlags.PositionProportional)
                .LayoutBounds(new Point(1, 0.5)),

                new BoxView
                {
                    Color = Colors.Grey,
                }.LayoutFlags(AbsoluteLayoutFlags.PositionProportional)
                .LayoutBounds(new Point(0.5, 1), new Size(100, 25)),

                new BoxView
                {
                    Color = Colors.Tan,
                }.LayoutFlags(AbsoluteLayoutFlags.All)
                .LayoutBounds(new Rect(0.5, 0.5, 1d/3d, 1d/3d))
            }
        };
    }
}
```

## Examples

You can find an example of these extension methods in action throughout the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui.Markup/blob/main/samples/CommunityToolkit.Maui.Markup.Sample/).

## API

You can find the source code for the `AbsoluteLayout` extension methods over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui.Markup/blob/main/src/CommunityToolkit.Maui.Markup/AbsoluteLayoutExtensions.cs).


