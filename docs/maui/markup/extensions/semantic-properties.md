---
title: SemanticProperties extensions - .NET MAUI Community Toolkit
author: bijington
description: The SemanticProperties extensions provide a series of extension methods that support the configuring of accessibility related settings.
ms.date: 09/14/2022
---

# SemanticProperties extensions

The `SemanticProperties` extensions provide a series of extension methods that support the configuring of accessibility related settings.

Semantic properties are used to define information about which controls should receive accessibility focus and which text should be read aloud to the user. Semantic properties are attached properties that can be added to any element to set the underlying platform accessibility APIs.

For further information on `SemanticProperties` and accessibility please refer to the [.NET MAUI documentation](/dotnet/maui/fundamentals/accessibility).

For information on other accessibility related extensions please refer to the [AutomationProperties extensions](automation-properties.md).

## SemanticDescription

The `SemanticDescription` method sets a short, descriptive string that the platforms screen reader uses to announce the `BindableObject`.

The following example demonstrates how to set the description on a new `Entry`:

```cs
new Entry().SemanticDescription("Enter your username.");
```

## SemanticHeadingLevel

The `SemanticDescription` method sets a heading level to enable the `BindableObject` to be marked as a heading to organize the UI and make it easier to navigate for the platform's screen reader.

The following example demonstrates how to set the heading level on a new `Entry`:

```cs
new Entry().SemanticHeadingLevel(SemanticHeadingLevel.Level5);
```

> [!IMPORTANT]
> Not all platforms support all `SemanticHeadingLevel` values, please refer to the [.NET MAUI documentation](/dotnet/maui/fundamentals/accessibility#heading-levels) for further information.

## SemanticHint

The `SemanticHint` method sets an additional context to that set in `SemanticDescription`, such as the purpose of the `BindableObject`.

The following example demonstrates how to set the hint on a new `Entry`:

```cs
new Entry().SemanticHint("The username field used to create a new account. This is a required field.");
```
