---
title: Object extensions - .NET MAUI Community Toolkit
author: brminnick
description: The Object Extensions provide a series of extension methods that support configuring any object.
ms.date: 11/05/2022
---

# Object extensions

The `Object` extensions provide a series of extension methods that support configuring any C# object (including reference types, value types, records, structs, etc).

The extensions offer the following methods:

## Assign

The `Assign` method makes it possible to assign a variable fluently. This is extremely useful for setting up a view-to-view binding.

This example binds the `TextColor` of the `Label` to be the inverse of its `BackgroundColor`:

```csharp
Content = new Label()
    .Assign(out var label)
    .Bind(
        Label.TextColorProperty,
        path: nameof(Label.BackgroundColor),
        source: label,
        converter: new ColorToInverseColorConverter());
```

## Invoke

The `Invoke` method allows you to perform an `Action` against. 

One benefit is the ability to fluently subscribe event handlers or configure other parts of your application.

This example subscribes the `SelectionChanged` event on the `CollectionView`.

```csharp
new CollectionView()
    .Invoke(collectionView => collectionView.SelectionChanged += HandleSelectionChanged);
```