---
title: AutomationProperties extensions - .NET MAUI Community Toolkit
author: bijington
description: The AutomationProperties extensions provide a series of extension methods that support the configuring of accessibility related settings.
ms.date: 09/14/2022
---

# AutomationProperties extensions

The `AutomationProperties` extensions provide a series of extension methods that support the configuring of accessibility related settings.

Automation properties are attached properties that can be added to any element to indicate how the element is reported to the underlying platform's accessibility framework.

For further information on `AutomationProperties` and accessibility please refer to the [.NET MAUI documentation](/dotnet/maui/fundamentals/accessibility#automation-properties).

For information on other accessibility related extensions please refer to the [SemanticProperties extensions](semantic-properties.md).

## AutomationExcludedWithChildren

The `AutomationExcludedWithChildren` method sets a value determining if the `BindableObject` and its children should be excluded from the accessibility tree.

The following example demonstrates how to exclude a new `VerticalStackLayout` and its children from the accessibility tree:

```cs
new VerticalStackLayout().AutomationExcludedWithChildren(true);
```

## AutomationIsInAccessibleTree

The `AutomationIsInAccessibleTree` method sets a value determining if the `BindableObject` is visible to screen readers.

The following example demonstrates how to exclude a new `VerticalStackLayout` from the accessibility tree:

```cs
new VerticalStackLayout().AutomationIsInAccessibleTree(false);
```
