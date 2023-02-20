---
title: GravatarImageSource - .NET MAUI Community Toolkit
author: GeorgeLeithead
description: "`GravatarImageSource` allows you to use as an Image source, a users Gravatar registered image via their email address."
ms.date: 09/16/2022
---

# GravatarImageSource

A _Gravatar_ (a "globally recognized avatar") is an image that can be used on multiple websites as your avatar — that is, an image that represents you. For example, a Gravatar can identify a person in a forum post, in a blog comment, and so on. (You can register your own Gravatar at the Gravatar website at [http://www.gravatar.com/](http://www.gravatar.com/).) If you want to display images next to people's names or email addresses, you can use GravatarImageSource.

## Syntax

### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

### Using the GravatarImageSource

The following example shows how to use `GravatarImageSource`:

```xaml
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.MyPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">
    <VerticalStackLayout>
        <Image>
            <Image.Source>
                <toolkit:GravatarImageSource
                    CacheValidity="1"
                    CachingEnabled="True"
                    Email="youremail@here.com"
                    Image="MysteryPerson" />
            </Image.Source>
        </Image>
    </VerticalStackLayout>
</ContentPage>
```

The equivalent C# code is:

```csharp
using CommunityToolkit.Maui.ImageSources;

partial class MyPage : ContentPage
{
	public MyPage()
	{
        Image myImage = new()
        {
            Source = new GravatarImageSource()
            {
                CacheValidity = TimeSpan.FromDays(1),
                CachingEnabled = true,
                Email = "youremail@here.com",
                Image= DefaultImage.MysteryPerson
            },
        };
		Content = myImage;
	}
}
```

## Properties

| Property | Type | Description |
|---|---|---|
| CacheValidity | `TimeSpan` | The `CacheValidity` property, of type `TimeSpan`, specifies how long the image will be stored locally for. The default value of this property is 1 day. |
| CachingEnabled | `bool` | The `CachingEnabled` property, of type `bool`, defines whether image caching is enabled. The default value of this property is `true`. |
| Email | `string?` | The `Email` property, of type `string?`, specifies the gravatar account email address.  If unset, the Gravatar image is rendered. If set and not found on Gravatar, the `Image` property image will be rendered. |
| Image | `DefaultImage` | The `Image` property, of type [`DefaultImage`](#set-default-image) is an enumeration that is used to specify the default image if the `email` is not found on Gravatar. |

These properties are backed by `BindableProperty` objects, which means that they can be targets of data bindings and styled.

## Set cache validity

The `CacheValidity` property is a `TimeSpan` that specifies how long the image will be stored locally for.

The following example sets the cache validity of a `GravatarImageSource`:

```xaml
<Image>
    <Image.Source>
        <toolkit:GravatarImageSource CacheValidity="1" />
    </Image.Source>
</Image>
```

The equivalent C# code is:

```csharp
Image myImage = new()
{
    Source = new GravatarImageSource()
    {
        CacheValidity = TimeSpan.FromDays(1),
    },
};
```

## Set caching enabled

The `CachingEnabled` property is a `bool` that defines whether image caching is enabled.

The following example sets caching to enabled for a `GravatarImageSource`:

```xaml
<Image>
    <Image.Source>
        <toolkit:GravatarImageSource CachingEnabled="True" />
    </Image.Source>
</Image>
```

The equivalent C# code is:

```csharp
Image myImage = new()
{
    Source = new GravatarImageSource()
    {
        CachingEnabled = true,
    },
};
```

## Set email

The `Email` property is a nullable `string`. If the property is null or empty, the default Gravatar image is rendered. If the email address has no matching Gravatar image, the `Image` property image is rendered.

The following example sets an email address that has a matching Gravatar image:

```xaml
<Image>
    <Image.Source>
        <toolkit:GravatarImageSource Email="dsiegel@avantipoint.com" />
    </Image.Source>
</Image>
```

The equivalent C# code is:

```csharp
Image myImage = new()
{
    Source = new GravatarImageSource()
    {
        Email = "dsiegel@avantipoint.com",
    },
};
```

The following example does not set an email address and will thus display the default Gravatar image.


```xaml
<Image>
    <Image.Source>
        <toolkit:GravatarImageSource />
    </Image.Source>
</Image>
```

The equivalent C# code is:

```csharp
Image myImage = new()
{
    Source = new GravatarImageSource(),
};
```

The following example sets an email address that has no matching Gravatar image and will thus display the default `Image` image.


```xaml
<Image>
    <Image.Source>
        <toolkit:GravatarImageSource Email="notregistered@emailongravitar.com" />
    </Image.Source>
</Image>
```

The equivalent C# code is:

```csharp
Image myImage = new()
{
    Source = new GravatarImageSource()
    {
        Email = "notregistered@emailongravitar.com",
    },
};
```
## Set default image

The `Image` property is an enumeration that is used to specify the default image if the `email` address has no matching Gravatar image.  The available options are:

- `MysteryPerson` (default) - A simple, cartoon-style silhouetted outline of a person (does not vary by email hash)
- `FileNotFound` - Do not load any image if none is associated with the email hash, instead return an HTTP 404 (File Not Found) response.
- `Identicon` - A geometric pattern based on an email hash.
- `MonsterId` - A generated 'monster' with different colours, faces, etc.
- `Wavatar` - Generated faces with differing features and backgrounds.
- `Retro` - Awesome generated, 8-bit arcade-style pixilated faces.
- `Robohash` - A generated robot with different colours, faces, etc.
- `Blank` - A transparent PNG image.

The following example sets the default image of a `GravatarImageSource`:

```xaml
<Image>
    <Image.Source>
        <toolkit:GravatarImageSource Email="notregistered@emailongravitar.com" Image="Retro" />
    </Image.Source>
</Image>
```

The equivalent C# code is:

```csharp
Image myImage = new()
{
    Source = new GravatarImageSource()
    {
        Email = "notregistered@emailongravitar.com",
        Image = DefaultImage.Retro
    },
};
```

## Set image size

By default, `GravatarImageSource` images are presented at 80px by 80px.  Image sizes can be between *1px and 2048px* and are taken from their parent view size properties.  Gravatar images are square, and the larger of the size properties defined will be taken.

The following example sets the size of the image control and thus the size of the Gravatar image requested will be 73px.

```xaml
<Image WidthRequest="72" HeightRequest="73">
    <Image.Source>
        <toolkit:GravatarImageSource Email="dsiegel@avantipoint.com" />
    </Image.Source>
</Image>
```

The equivalent C# code is:

```csharp
Image myImage = new()
{
    Source = new GravatarImageSource()
    {
        Email = "dsiegel@avantipoint.com",
    },
    HeightRequest = 72,
    HeightRequest = 73,
};
```

## Examples

You can find examples of this control in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/ImageSources/GravatarImageSourcePage.xaml).

## API

You can find the source code for `GravatarImageSource` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/ImageSources/GravatarImageSource.shared.cs).