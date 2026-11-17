---
title: Placeholder extensions - .NET MAUI Community Toolkit
author: TheCodeTraveler
description: The Placeholder extensions provide a series of extension methods that support configuring InputView and SearchHandler controls
ms.date: 07/21/2026
---

# Placeholder extensions

The `Placeholder` extensions provide a series of extension methods that support configuring controls that offer a placeholder: `InputView` controls (such as `Editor`, `Entry`, and `SearchBar`) and `SearchHandler`.

The extensions offer the following methods:

## PlaceholderColor

The `PlaceholderColor` method sets the `PlaceholderColor` property on an `InputView` or `SearchHandler` element.

The following example sets the `PlaceholderColor` to `Colors.Red`:

```csharp
new Entry().PlaceholderColor(Colors.Red);
```

## Placeholder

The `Placeholder` method sets the `Placeholder` property on an `InputView` or `SearchHandler` element.

The following example sets the `Placeholder` to `"Enter Text"`:

```csharp
new Entry().Placeholder("Enter Text");
```

There is a second, overloaded, method for `Placeholder` that will set both the `Placeholder` and `PlaceholderColor` properties on an `InputView` or `SearchHandler` element.

The following example sets the `Placeholder` to `"Address, City, State"` and the `PlaceholderColor` to `Colors.Grey`:

```csharp
new Editor().Placeholder("Address, City, State", Colors.Grey);
```
