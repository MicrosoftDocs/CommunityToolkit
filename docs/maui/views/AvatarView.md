---
title: AvatarView - .NET MAUI Community Toolkit
author: GeorgeLeithead
description: "AvatarView is a control for displaying an image or user's initials avatar."
ms.date: 07/11/2022
---

# AvatarView

The CommunityToolKit MAUI `AvatarView` displays text and image-based avatars.  Avatars can be text, image, colored, shaped and supports shadow and gestures.

`AvatarView` defines the following properties:

- `BackgroundColor`, of type `Color`, describes the background color of the AvatarView. The default value of this property is White.
- `BorderColor`, of type `Color`, describes the border color of the AvatarView.
- `BorderWidth`, of type `double`, defines the width of the AvatarView's border.  The default value for this property is 1.0.
- `CharacterSpacing`, of type `double`, defines the spacing between characters of the AvatarViews's text.
- `CornerRadius`, of type `CornerRadius`, which defines the corner radius of the `AvatarView`. This property can be set to a single `double` uniform corner radius value, or a `CornerRadius` structure defined by four `double` values that are applied to the top left, top right, bottom left, and bottom right of the `AvatarView`.  The default value of this property is a device-independent unit of 24.
- `FontAttributes`, of type `FontAttributes`, determines text style.
- `FontAutoScalingEnabled`, of type `bool`, defines whether the AvatarView text will reflect scaling preferences set in the operating system. The default value of this property is `true`.
- `FontFamily`, of type `string`, defines the font family.
- `FontSize`, of type `double`, defines the font size.  The default value for this property is a device-independent unit of 14.
- `ImageSource`, of type `ImageSource`, specifies an image to display as the content of the AvatarView.
- `Padding`, of type `Thickness`, represents the distance between the avatar border and its text or image element.
- `Text`, of type `string`, defines the text displayed as the content of the AvatarView.  This default value for this property is '?'.
- `TextColor`, of type `Color`, describes the color of the AvatarView's text.
- `TextTransform`, of type `TextTransform`, defines the casing of the AvatarView's text.

These properties are backed by `BindableProperty` objects, which means that they can be targets of data bindings and styled.

For information about specifying fonts on an `AvatarView`, see [Fonts](/dotnet/maui/user-interface/fonts.md).

For information about specifying shadows on an `AvatarView`, see [Shadows](/dotnet/maui/user-interface/shadow.md)


> [!IMPORTANT]
> `AvatarView` will use the default `WidthRequest` and `HeightRequest` of 48 unless the size of the `AvatarView` is constrained by its layout, or the `HeightRequest` or `WidthRequest` property of the `AvatarView` is specified. The `WidthRequest` and `HeightRequest` properties are measured in device-independent units.

## Create an AvatarView

The following example shows how to create an `AvatarView`:

```xaml
<views:AvatarView
	BackgroundColor="Blue"
	BorderColor="Red"
	BorderWidth="1"
	CornerRadius="24, 0, 0, 24"
	FontAttributes="Bold"
	FontSize="Large"
	HeightRequest="48"
	Padding="0"
	Text="ZS"
	TextColor="Yellow"
	WidthRequest="64" />
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

AvatarView avatarView = new AvatarView
{
	BackgroundColor = Colors.Blue,
	BorderColor = Colors.Red,
	BorderWidth = 1,
	CornerRadius = new CornerRadius(24, 0, 0, 24),
	FontAttributes = FontAttributes.Bold,
	FontSize = 24,
	HeightRequest = 48,
	Padding = 0,
	Text = "ZS", // Zoe Saldana
	TextColor = Colors.Yellow,
	WidthRequest = 64,
};
```

In this example, a text `AvatarView` with rounded top-left and bottom-right corners is drawn whose `CornerRadius` is set for each corner along with the `HeightRequest` and `WidthRequest`, and the `BackgroundColor`, `BorderColor`, `BorderWidth` and `TextColor` are set along with the `FontSize` and `FontAttributes`.

![AvatarView example](../images/AvatarView/AvatarViewBasic.png "Example AvatarView.")

## Set background color

`AvatarView` can be set to use a specific background color via the `BackgroundColor` property.

The following example sets the background color of an `AvatarView`:

```xaml
<views:AvatarView BackgroundColor="Red" Text="BC" />
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

AvatarView avatarView = new AvatarView
{
	Text = "BC",
	BackgroundColor = Colors.Red,
};
```

For more information about colors, see [Colors](/dotnet/maui/user-interface/graphics/colors.md).

## Set border color

`AvatarView` can be set to use a specific border color via the `BorderColor` property.

The following example sets the border color of an `AvatarView`:

```xaml
<views:AvatarView BorderColor="Blue" Text="BC" />
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

AvatarView avatarView = new AvatarView
{
	Text = "BC",
	BorderColor = Colors.Blue,
};
```

For more information about colors, see [Colors](/dotnet/maui/user-interface/graphics/colors.md).

## Set border thickness

`AvatarView` can be set to use a specific border thickness via the `BorderWidth` property.  If you set `BorderWidth` to 0 then the border around the avatar is not shown.

The following example sets the border width of an `AvatarView`:

```xaml
<views:AvatarView BorderWidth="2" Text="BW" />
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

AvatarView avatarView = new AvatarView
{
	Text = "BW",
	BorderWidth = 2,
};
```

## Set character spacing

Character spacing can be applied to `AvatarView` object `Text` property by setting the `CharacterSpacing` property to a `double` value:

```xaml
<views:AvatarView CharacterSpacing="10" Text="CS" />
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

AvatarView avatarView = new AvatarView
{
	Text = "CS",
	CharacterSpacing = 10,
};
```

The result is that characters in the text displayed by the `AvatarView` are spaced `CharacterSpacing` device-independent units apart.

## Set the corner radius

`AvatarView` can be set to use a .NET MAUI `CornerRadius` property.  The `CornerRadius` property specifies the radius used to round the corners of the control.

The following example sets the corner radius of an `AvatarView` such that each of the four corners have a specified radius:

```xaml
<views:AvatarView CornerRadius="8, 12, 16, 20" HeightRequest="48" Text="CR" WidthRequest="48" />
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

AvatarView avatarView = new AvatarView
{
	CornerRadius = new(8, 12, 16, 20),
	HeightRequest = 48,
	Text = "CR",
	WidthRequest = 48,
};
```

The following example sets the corner radius of an `AvatarView` such that all four corners have the same radius:

```xaml
<views:AvatarView CornerRadius="8" HeightRequest="48" Text="CR" WidthRequest="48" />
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

AvatarView avatarView = new AvatarView
{
	CornerRadius = new(8),
	HeightRequest = 48,
	Text = "CR",
	WidthRequest = 48,
};
```

## Set image source

The `AvatarView` class defines an `ImageSource` property that allows you to display a bitmap image within the avatar.  If you set a `ImageSource` property, then the image is displayed instead of any `Text` property value.  The `ImageSource` property is of type `ImageSource`, which means that the bitmaps can be loaded from a file embedded resource, URL, or stream.

The following example sets the `ImageSource` of an `AvatarView` to use an embedded resource:

```xaml
<views:AvatarView ImageSource="Avatar_Icon_.png" Text="IS" />
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

AvatarView avatarView = new AvatarView
{
	ImageSource = "Avatar_Icon_.png",
	Text = "IS",
};
```

The following example sets the `ImageSource` of an `AvatarView` to use a URL:

```xaml
<views:AvatarView ImageSource="https://aka.ms/campus.jpg" Text="IS" />
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

AvatarView avatarView = new AvatarView
{
	ImageSource = "https://aka.ms/campus.jpg",
	Text = "IS",
};
```

## Set padding

`AvatarView` can be set to use the `Padding` property which represents the distance between the avatar border and its text or image.

The following example sets the `Padding` of an `AvatarView`:

```xaml
<views:AvatarView Padding="2" Text="PA" />
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

AvatarView avatarView = new AvatarView
{
	Padding = 2,
	Text = "PA",
};
```

## Set text

`AvatarView` can be set to use specific text for the avatar via the `Text` property.  If the `ImageSource` property is set, then the `Text` property is not shown.

The following example sets the `Text` of an `AvatarView`:

```xaml
<views:AvatarView Text="ST" />
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

AvatarView avatarView = new AvatarView
{
	Text = "ST",
};
```

## Set text color

`AvatarView` can be set to use a specific text color via the `TextColor` property.

The following example sets the text color of an `AvatarView`:

```xaml
<views:AvatarView Text="TC" TextColor="Green" />
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

AvatarView avatarView = new AvatarView
{
	Text = "TC",
	TextColor = Colors.Green,
};
```

For more information about colors, see [Colors](/dotnet/maui/user-interface/graphics/colors.md).


## Transform text

An `AvatarView` can transform the casing of its text, stored in the `Text` property, by setting the `TextTransform` property to a value of the `TextTransform` enumeration. This enumeration has four values:

- `None` indicates that the text won't be transformed.
- `Default` indicates that the default behavior for the platform will be used. This is the default value of the `TextTransform` property.
- `Lowercase` indicates that the text will be transformed to lowercase.
- `Uppercase` indicates that the text will be transformed to uppercase.

The following example shows transforming text to uppercase:

```xaml
<views:AvatarView TextTransform="Uppercase" Text="Tt" />
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.Views;

AvatarView avatarView = new AvatarView
{
	Text = "Tt",
	TextTransform = TextTransform.Uppercase,
};
```

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/AvatarViewPage.xaml.cs).

## API

You can find the source code for `AvatarView` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Views/AvatarView.shared.cs).