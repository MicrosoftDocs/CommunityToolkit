---
title: Image extensions - .NET MAUI Community Toolkit
author: TheCodeTraveler
description: The Image extensions provide a series of extension methods that support configuring Image and ImageButton controls
ms.date: 07/21/2026
---

# Image extensions

The `Image` extensions provide a series of extension methods that support configuring `Image` and `ImageButton` controls.

The extensions offer the following methods:

## Source

The `Source` method sets the `Source` property on an `Image` or `ImageButton` element.

The following example sets the `Source` to `"dotnet_bot"`:

```csharp
new Image().Source("dotnet_bot");
```

## Aspect

The `Aspect` method sets the `Aspect` property on an `Image` or `ImageButton` element.

The following example sets the `Aspect` to `Aspect.AspectFill`:

```csharp
new Image().Aspect(Aspect.AspectFill);
```

## IsOpaque

The `IsOpaque` method sets the `IsOpaque` property on an `Image` or `ImageButton` element.

The following example sets the `IsOpaque` to `true`:

```csharp
new Image().IsOpaque(true);
```
