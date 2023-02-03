---
title: ProgressBarAnimationBehavior - .NET MAUI Community Toolkit
author: cliffagius
description: "The ProgressBar Animation Behavior animates a ProgressBar from its current Progress value to a provided value over time."
ms.date: 05/02/2022
---

# ProgressBarAnimationBehavior

The ProgressBar Animation Behavior animates a `ProgressBar` from its current Progress value to a provided value over time. The method accepts a `Double` progress value, a `uint` duration in milliseconds and an `Easing` enum value.

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ProgressBarAnimationBehavior

The `ProgressBarAnimationBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyLittleApp.MainPage">
     
        <Label Text="The ProgressBarAnimationBehavior is a behavior that animates a ProgressBar" />

        <ProgressBar>
            <ProgressBar.Behaviors>
                <toolkit:ProgressBarAnimationBehavior
                    x:Name="ProgressBarAnimationBehavior"
                    Progress="{Binding Progress}"
                    Length="250"/>
            </ProgressBar.Behaviors>
        </ProgressBar>
</ContentPage>
```

### C#

The `ProgressBarAnimationBehavior` can be used as follows in C#:

```csharp
class ProgressBarAnimationBehaviorPage : ContentPage
{
    public ProgressBarAnimationBehaviorPage()
    {
        var progressBar = new ProgressBar();

        var behavior = new ProgressBarAnimationBehavior()
        {
            Progress = 0.75,
            Length = 250
        };

        progressBar.Behaviors.Add(behavior);

        Content = progressBar;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class ProgressBarAnimationBehaviorPage : ContentPage
{
    public ProgressBarAnimationBehaviorPage()
    {
        Content = new ProgressBar()
        .Behaviors(new ProgressBarAnimationBehavior
        {
            Progress = 0.75,
            Length = 250
        });           
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| Progress | Double  | New Progress value to animate to as a percentage with 1 being 100% so 0.75 is 75% |
| Length | uint | Duration in milliseconds |
| Easing | enum | `enum` that controls the `Easing`, allows you to specify a transfer function that controls how animations speed up or slow down. You can find more details on [Easing here](/dotnet/maui/user-interface/animation/easing) |

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/ProgressBarAnimationBehaviorPage.xaml).

## API

You can find the source code for `ProgressBarAnimationBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/ProgressBarAnimationBehavior.shared.cs).
