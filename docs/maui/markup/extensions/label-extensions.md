---
title: Label extensions - .NET MAUI Community Toolkit
author: brminnick
description: The Label extensions provide a series of extension methods that support configuring a Label.
ms.date: 05/18/2022
---

# Label extensions

The `Label` extensions provide a series of extension methods that support configuring a `Label`.

## FormattedText

The `FormattedText` method allows us to assign multiple `Span`s to the `Label.FormattedTextProperty`.

The following example demonstrates how to add multiple `Span`s to a `Label` using `.FormattedText()`:

```cs
new Label().FormattedText(new[] 
{
    new Span { Text = "Here is a link to the docs: " },
    new Span { Text = "https://learn.microsoft.com/", TextDecorations = TextDecorations.Underline, TextColor = Colors.Blue }
});
```
