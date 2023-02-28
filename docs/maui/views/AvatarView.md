---
title: AvatarView - .NET MAUI Community Toolkit
author: GeorgeLeithead
description: "The `AvatarView` is a control for displaying a user's avatar image or their initials."
ms.date: 07/11/2022
---

# AvatarView

The CommunityToolKit MAUI `AvatarView` is a control for displaying a user's avatar image or their initials.  Avatars can be text, image, colored, shaped and supports shadow and gestures.

## Syntax

### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

### Using the AvatarView

The following example shows how to create an `AvatarView`:

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.MyPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    <VerticalStackLayout>
        <toolkit:AvatarView Text="ZS" />
    </VerticalStackLayout>
</ContentPage>
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

partial class MyPage : ContentPage
{
	public MyPage()
	{
		AvatarView avatarView = new()
		{
			Text = "ZS",
		};

		Content = avatarView;
	}
}
```

## Properties

| Property | Type | Description |
|---|---|---|
| BackgroundColor | `Color` | The `BackgroundColor` property is a Color that determines the background color of the control. If unset, the background will be the default Color object, which renders as White. |
| BorderColor | `Color` | The `BorderColor` property is a Color that determines the border color of the control.  If unset, the border will be the default Color object, which renders as Black. |
| BorderWidth | `double` | The `BorderWidth` property is a double that determines the rendered width of the control border.  If unset, the border width will be the default, which renders as 1.0. |
| CornerRadius | `CornerRadius` | The `CornerRadius` property is a CornerRadius that determines the shape of the control.  It can be set to a single `double` uniform corner radius value, or a `CornerRadius` structure defined by four `double` values that are applied to the top left, top right, bottom left, and bottom right of the control.  This property is measured in device-independent units.  If unset, the corner radius will be the default CornerRadius object, which renders as 24. |
| ImageSource | `ImageSource` | The `ImageSource` property is an ImageSource that determines the image of the control.  It can be set to an image retrieved from a file, embedded resource, URI, or stream. If unset, the control will render the `Text` property. |
| Padding | `Thickness` | The `Padding` property is a Thickness that represents the distance between control border and the `Text` or `ImageSource`.  If unset, the padding will be the default Thickness object, which is 1. |
| Text | `string` | The `Text` property is a string that determines the text of the control.  If unset, the text will be the default, which renders as '?'. |
| TextColor | `Color` | The `TextColor` property is a Color that determines the text color of the control.  If unset, the text will be the default Colour object. |

These properties are backed by `BindableProperty` objects, which means that they can be targets of data bindings and styled.

For information about specifying fonts on an `AvatarView`, see [Fonts](/dotnet/maui/user-interface/fonts).

For information about specifying shadows on an `AvatarView`, see [Shadows](/dotnet/maui/user-interface/shadow)


> [!IMPORTANT]
> `AvatarView` will use the default `WidthRequest` and `HeightRequest` of 48 unless the size of the `AvatarView` is constrained by its layout, or the `HeightRequest` or `WidthRequest` property of the `AvatarView` is specified. The `WidthRequest` and `HeightRequest` properties are measured in device-independent units.

## Set background color

The `BackgroundColor` property is a Color that determines the background color of the control.

The following example sets the background color of an `AvatarView`:

```xaml
<toolkit:AvatarView BackgroundColor="Red" Text="BC" />
```

The equivalent C# code is:

```csharp
AvatarView avatarView = new()
{
	Text = "BC",
	BackgroundColor = Colors.Red,
};
```

For more information about colors, see [Colors](/dotnet/maui/user-interface/graphics/colors).

## Set border color

The `BorderColor` property is a Color that determines the border color of the control.

The following example sets the border color of an `AvatarView`:

```xaml
<toolkit:AvatarView BorderColor="Blue" Text="BC" />
```

The equivalent C# code is:

```csharp
AvatarView avatarView = new()
{
	Text = "BC",
	BorderColor = Colors.Blue,
};
```

For more information about colors, see [Colors](/dotnet/maui/user-interface/graphics/colors).

## Set border width

The `BorderWidth` property is a double that determines the rendered width of the control border.

The following example sets the border width of an `AvatarView`:

```xaml
<toolkit:AvatarView BorderWidth="2" Text="BW" />
```

The equivalent C# code is:

```csharp
AvatarView avatarView = new()
{
	Text = "BW",
	BorderWidth = 2,
};
```

## Set the corner radius

The `CornerRadius` property is a CornerRadius that determines the shape of the control.  It can be set to a single `double` uniform corner radius value, or a `CornerRadius` structure defined by four `double` values that are applied to the top left, top right, bottom left, and bottom right of the control.

The following example sets the corner radius of an `AvatarView` such that each of the four corners have a specified radius:

```xaml
<toolkit:AvatarView CornerRadius="8, 12, 16, 20" HeightRequest="48" Text="CR" WidthRequest="48" />
```

The equivalent C# code is:

```csharp
AvatarView avatarView = new()
{
	CornerRadius = new(8, 12, 16, 20),
	HeightRequest = 48,
	Text = "CR",
	WidthRequest = 48,
};
```

The following example sets the corner radius of an `AvatarView` such that all four corners have the same radius:

```xaml
<toolkit:AvatarView CornerRadius="8" HeightRequest="48" Text="CR" WidthRequest="48" />
```

The equivalent C# code is:

```csharp
AvatarView avatarView = new()
{
	CornerRadius = new(8),
	HeightRequest = 48,
	Text = "CR",
	WidthRequest = 48,
};
```

## Set image source

The `ImageSource` property is an ImageSource that determines the image of the control.  It can be set to an image retrieved from a file, embedded resource, URI, or stream.

The following example sets the `ImageSource` of an `AvatarView` to use an embedded resource:

```xaml
<toolkit:AvatarView ImageSource="Avatar_Icon_.png" Text="IS" />
```

The equivalent C# code is:

```csharp
AvatarView avatarView = new()
{
	ImageSource = "Avatar_Icon_.png",
	Text = "IS",
};
```

The following example sets the `ImageSource` of an `AvatarView` to use a URL:

```xaml
<toolkit:AvatarView ImageSource="https://aka.ms/campus.jpg" Text="IS" />
```

The equivalent C# code is:

```csharp
AvatarView avatarView = new()
{
	ImageSource = "https://aka.ms/campus.jpg",
	Text = "IS",
};
```

## Set padding

The `Padding` property is a Thickness that represents the distance between control border and the `Text` or `ImageSource`.

The following example sets the `Padding` of an `AvatarView`:

```xaml
<toolkit:AvatarView Padding="2" Text="PA" />
```

The equivalent C# code is:

```csharp
AvatarView avatarView = new()
{
	Padding = 2,
	Text = "PA",
};
```

## Set text

 The `Text` property is a string that determines the text of the control.

The following example sets the `Text` of an `AvatarView`:

```xaml
<toolkit:AvatarView Text="ST" />
```

The equivalent C# code is:

```csharp
AvatarView avatarView = new()
{
	Text = "ST",
};
```

## Set text color

The `TextColor` property is a Color that determines the text color of the control.

The following example sets the text color of an `AvatarView`:

```xaml
<toolkit:AvatarView Text="TC" TextColor="Green" />
```

The equivalent C# code is:

```csharp
AvatarView avatarView = new()
{
	Text = "TC",
	TextColor = Colors.Green,
};
```

For more information about colors, see [Colors](/dotnet/maui/user-interface/graphics/colors).

## Examples

You can find examples of this control in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/AvatarView).

## API

You can find the source code for `AvatarView` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Views/AvatarView.shared.cs).
