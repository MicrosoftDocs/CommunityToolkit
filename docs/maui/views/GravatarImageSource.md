---
title: GravatarImageSource - .NET MAUI Community Toolkit
author: GeorgeLeithead
description: "The `AvatarView` is a control for displaying a user's avatar image or their initials."
ms.date: 08/05/2022
---

# GravatarImageSource

A _Gravatar_ (a "globally recognized avatar") is an image that can be used on multiple websites as your avatar — that is, an image that represents you. For example, a Gravatar can identify a person in a forum post, in a blog comment, and so on. (You can register your own Gravatar at the Gravatar website at [http://www.gravatar.com/](http://www.gravatar.com/).) If you want to display images next to people's names or email addresses, you can use GravatarImageSource.

## Syntax
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
                    Email="youremail@here"
                    Image="MysteryPerson" />
            </Image.Source>
        </Image>
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
        Image myImage = new()
        {
            Source = new GravatarImageSource()
            {
                CacheValidity = TimeSpan.FromDays(1),
                CachingEnabled = true,
                Email = "youremail@here",
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
| Email | `string?` | The `Email` property, of type `string?`, specifies the gravitar account email address.  If unset, the image will render the Gravatar image. If set and not found on Gravatar, the image will render from the `Image` property. |
| Image | `DefaultImage` | The `Image` property, of type `DefaultImage` is an enumeration that is used to specify the default image if the `email` is not found on Gravatar. |

These properties are backed by `BindableProperty` objects, which means that they can be targets of data bindings and styled.

## Set cache validity

The `CacheValidity` property is a `TimeSpan` that specifies how long the image will be stored locally for..

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

## Set default image

The `Image` property is an enumeration that is used to spedify the default image if the `email` is not found on Gravatar.  The available options are:

- MysteryPerson (default) - A simple, cartoon-style silhouetted outline of a person (does not vary by email hash)
- FileNotFound - Do not load any image if none is associated with the email hash, instead return an HTTP 404 (File Not Found response.
- Identicon - A geometric pattern based on an email hash.
- MonsterId - A generated 'monster' with different colours, faces, etc.
- Wavatar - Generated faces with differing features and backgrounds.
- Retro - Awesome generated, 8-bit arcade-style pixilated faces.
- Robohash - A generated robot with different colours, faces, etc.
- Blank - A transparent PNG image.

The following example sets the default image of a `GravatarImageSource`:

```xaml
<Image>
    <Image.Source>
        <toolkit:GravatarImageSource Email="notregistered@emailongravitar" Image="Retro" />
    </Image.Source>
</Image>
```

The equivalent C# code is:

```csharp
Image myImage = new()
{
    Source = new GravatarImageSource()
    {
        Email = "notregistered@emailongravitar",
        Image = DefaultImage.Retro
    },
};
```


## Examples

You can find examples of this control in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/GravatarImageSourcePage.xaml).

## API

You can find the source code for `GravatarImageSource` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Views/GravatarImageSource.shared.cs).