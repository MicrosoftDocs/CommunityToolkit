---
title: FadeAnimation - .NET MAUI Community Toolkit
author: bijington
description: The FadeAnimation provides the ability to animate the opacity of a VisualElement from it's original opacity, to a specified new opacity and then back to the original.
ms.date: 09/16/2022
---

# FadeAnimation

The `FadeAnimation` provides the ability to animate the opacity of a `VisualElement` from it's original opacity, to a specified new opacity and then back to the original.

## Syntax

### XAML

For use within XAML the `FadeAnimation` must be used in conjunction with the [`AnimationBehavior`](../behaviors/animation-behavior.md).

### C#

The `FadeAnimation` can be used as follows in C#:

```csharp
public async void Animate()
{
    var label = new Label();
    
    var fadeAnimation = new FadeAnimation();
    
    await fadeAnimation.Animate(label);
}
```

## Examples

You can find an example of this animation in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/AnimationBehaviorPage.xaml).

## API

You can find the source code for `FadeAnimation` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Animations/FadeAnimation.shared.cs).
