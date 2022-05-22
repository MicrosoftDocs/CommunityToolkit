---
title: Placeholder extensions - .NET MAUI Community Toolkit
author: brminnick
description: The Placeholder extensions provide a series of extension methods that support configuring IPlaceholder controls
ms.date: 03/28/2022
---

# Placeholder extensions

The `Placeholder` extensions provide a series of extension methods that support configuring `IPlaceholder` controls.

The extensions offer the following methods:

## PlaceholderColor

The `PlaceholderColor` method sets the `PlaceholderColor` property on an `IPlaceholder` element.

The following example sets the `PlaceholderColor` to `Colors.Red`:

```csharp
new Entry().PlaceholderColor(Colors.Red);
```

## Placeholder

The `Placeholder` method sets the `Placeholder` property on an `IPlaceholder` element.

The following example sets the `Placeholder` to `"Enter Text"`:

```csharp
new Entry().Placeholder("Enter Text");
```

There is a second, overloaded, method for `Placeholder` that will set both the `Placeholder` and `PlaceholderColor` properties on an `IPlaceholder` element.

The following example sets the `Placeholder` to `"Address, City, State"` and the `PlaceholderColor` to `Colors.Grey`:

```csharp
new Editor().Placeholder("Address, City, State", Colors.Grey);
```
