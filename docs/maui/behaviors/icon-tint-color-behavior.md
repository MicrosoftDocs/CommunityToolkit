---
title: IconTintColorBehavior - .NET MAUI Community Toolkit
author: vhugogarcia
description: "The IconTintColorBehavior is a behavior allows you to tint an image."
ms.date: 06/27/2022
---

# IconTintColorBehavior

The `IconTintColorBehavior` is a `behavior` allows you to tint an image.

> [!IMPORTANT]
> The `IconTintColorBehavior` is not supported on Windows.

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the IconTintColorBehavior

The `IconTintColorBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyLittleApp.MainPage">
    
    <Image Source="shield.png">
        <Image.Behaviors>
            <toolkit:IconTintColorBehavior TintColor="Red" />
        </Image.Behaviors>
    </Image>

</ContentPage>
```

### C#

The `IconTintColorBehavior` can be used as follows in C#:

```csharp
class IconTintColorBehaviorPage : ContentPage
{
    public IconTintColorBehaviorPage()
    {
        var img = new Image();

        var behavior = new IconTintColorBehavior
        {
            TintColor = Color.Red
        };

        img.Behaviors.Add(behavior);

        Content = entry;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class IconTintColorBehaviorPage : ContentPage
{
    public IconTintColorBehaviorPage()
    {
        Content = new Image()
        .Behaviors(new IconTintColorBehavior
        {
            Tintcolor = Color.Red
        });                 
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| TintColor | Color | The `Color` name from the Microsoft.Maui.Graphics namespace. |

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/IconTintColorBehaviorPage.xaml).

## API

You can find the source code for `IconTintColorBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/PlatformBehaviors/IconTintColor/IconTintColorBehavior.shared.cs).
