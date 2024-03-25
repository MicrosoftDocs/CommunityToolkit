---
title: ImageTouchBehavior - .NET MAUI Community Toolkit
author: bijington
description: The ImageTouchBehavior extends the TouchBehavior by providing the ability to customize Image elements based on touch, mouse click and hover events.
ms.date: 03/25/2024
---

# ImageTouchBehavior

The `ImageTouchBehavior` extends the `TouchBehavior` by providing the ability to customize `Image` elements based on touch, mouse click and hover events. The `ImageTouchBehavior` implementation makes it possible to customize the `Source` property of the `Image` element that it is attached to.

> [!NOTE]
> For further customization options in the `ImageTouchBehavior` please refer to the [`TouchBehavior`](./touch-behavior.md) implementation that this `Behavior` extends.

## Syntax

The following examples show how to add the `ImageTouchBehavior` to an `Image` and toggle between the `DefaultImageSource` and the `PressedImageSource` when the users interacts with the image by either pressing their finger or clicking with the mouse on the `Image`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the AnimationBehavior

```xaml
<ContentPage 
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
    x:Class="CommunityToolkit.Maui.Sample.Pages.Behaviors.TouchBehaviorPage"
    x:Name="Page">

    <Image HeightRequest="100" WidthRequest="100">
        <Image.Behaviors>
            <toolkit:ImageTouchBehavior
                Command="{Binding Source={x:Reference Page}, Path=BindingContext.IncreaseTouchCountCommand}"
                DefaultImageSource="button.png"
                PressedImageSource="button_pressed.png" />
        </Image.Behaviors>
    </Image>

</ContentPage>
```

### C#

The `ImageTouchBehavior` can be used as follows in C#:

```csharp
class TouchBehaviorPage : ContentPage
{
    public TouchBehaviorPage()
    {
        InitializeComponent();

        var image = new Image
        {
            HeightRequest = 100,
            WidthRequest = 100
        };

        var imageTouchBehavior = new ImageTouchBehavior
        {
            Command = ((TouchBehaviorBehaviorViewModel)BindingContext).IncreaseTouchCountCommand,
            DefaultImageSource = "button.png",
            PressedImageSource = "button_pressed.png"
        };

        image.Behaviors.Add(imageTouchBehavior);

        Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class TouchBehaviorPage : ContentPage
{
    public TouchBehaviorPage()
    {
        Content = new Image()
            .Size(100, 100)
            .Behaviors(new ImageTouchBehavior
            {
                Command = ((TouchBehaviorBehaviorViewModel)BindingContext).IncreaseTouchCountCommand,
                DefaultImageSource = "button.png",
                PressedImageSource = "button_pressed.png"
            });
    }
}
```

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/TouchBehaviorPage.xaml).

## API

You can find the source code for `ImageTouchBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/ImageTouchBehavior.shared.cs).
