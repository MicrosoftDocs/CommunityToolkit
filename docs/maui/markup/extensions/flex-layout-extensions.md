---
title: FlexLayout extensions - .NET MAUI Community Toolkit
author: danielftz
description: The FlexLayout extensions provide a series of extension methods that support positioning Views in FlexLayouts.
ms.date: 04/06/2022
---

# FlexLayout extensions

[!INCLUDE [docs under construction](../../includes/preview-note.md)]

The FlexLayout extensions provide a series of extension methods that support positioning `View`s in `FlexLayout`s.

The extensions offer the following methods:

## AlignSelf

The `AlignSelf` extension method allows you to set how a `View` in `FlexLayout` is aligned on the cross axis. Setting this property overrides the `AlignItems` property set on the parent `FlexLayout` itself. For further detail refer to the [Microsoft documentation](/dotnet/maui/user-interface/layouts/layouts/flexlayout#alignself).

## Basis

The `Basis` extension method allows you to set the amount of space that's allocated to a `View` in `FlexLayout` on the main axis. The size can be specified in device-independent units, as a percentage of the size of the `FlexLayout` or based on the `View`'s requested width or height. For further detail refer to the [Microsoft documentation](/dotnet/maui/user-interface/layouts/flexlayout#basis).

## Grow

The `Grow` extension method specifies the amount of available spacea `View` in `FlexLayout` should use on the main axis. For further detail refer to the [Microsoft documentation](/dotnet/maui/user-interface/layouts/flexlayout#grow).

## Order

The `Order` extension method allows you to change the order that the children of the FlexLayout are arranged.  Setting this property overrides the order that it appears in the `Children` collection. For further detail refer to the[Microsoft documentation](/dotnet/maui/user-interface/layouts/flexlayout#order).

## Shrink

The `Shrink` extension method allows you to indicate which `View` in `FlexLayout` is given priority in being displayed at their full sizes when the aggregate size of `Children` is greater than 
on the main axis. For further detail refer to the[Microsoft documentation](/dotnet/maui/user-interface/layouts/flexlayout#shrink).


## Syntax

```csharp
using Microsoft.Maui.Layouts;
using CommunityToolkit.Maui.Markup;
using Microsoft.Maui.Controls;
using Microsoft.Maui.Graphics;

namespace CommunityToolkit.Maui.Markup.Sample.Pages;

public class FlexLayoutSamplePage : ContentPage
{
	public FlexLayoutSamplePage()
	{
		Content = new FlexLayout
		{
			Direction = FlexDirection.Column,
			AlignContent = FlexAlignContent.Center,
			Children =
				{
					new Label
					{
						Text = "HEADER",
						FontSize = 25,
						BackgroundColor = Colors.Aqua,
					}.TextCenterHorizontal()
					.AlignSelf(FlexAlignSelf.Stretch),

					new FlexLayout()
					{
						Children =
						{
							new Label
							{
								Text = "Content",
								FontSize = 20,
								BackgroundColor = Colors.Grey
							}.Grow(1)
							.TextCenterHorizontal()
							.AlignSelf(FlexAlignSelf.Stretch),

							new BoxView
							{
								Color = Colors.Blue,
							}.Basis(50)
							.Order(-1),

							new BoxView
							{
								Color= Colors.Green,
							}.Basis(50)
						}

					}.Grow(1)
					.AlignSelf(FlexAlignSelf.Stretch),

					new Label
					{
						Text = "FOOTER",
						FontSize = 20,
						BackgroundColor = Colors.Pink,
					}.TextCenterHorizontal()
					.AlignSelf(FlexAlignSelf.Stretch)
				}
		};
	}
}


```

## API

You can find the source code for the `FlexLayout` extension methods over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui.Markup/blob/main/src/CommunityToolkit.Maui.Markup/FlexLayoutExtensions.cs).