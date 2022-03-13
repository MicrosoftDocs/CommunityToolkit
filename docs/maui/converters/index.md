---
title: Converters - .NET MAUI Community Toolkit
author: bijington
description: The .NET MAUI Community Toolkit is a collection of reusable elements for application development with .NET MAUI, including animations, behaviors, converters, effects, and helpers.
ms.date: 03/13/2022
---

# What is a Converter?

.NET Multi-platform App UI (.NET MAUI) data bindings usually transfer data from a source property to a target property, and in some cases from the target property to the source property. This transfer is straightforward when the source and target properties are of the same type, or when one type can be converted to the other type through an implicit conversion. When that is not the case, a type conversion must take place.

For further information on Converters please refer to the [.NET MAUI documentation](/dotnet/maui/fundamentals/data-binding/converters).

# .NET MAUI Community Toolkit Converters

The .NET MAUI Community Toolkit provides a collection of pre-built, reusable converters to make developers lives easier. Here are the converters provided by the toolkit:

| Converter | Description |
| --------- | ----------- |
| [`EqualConverter`](equal-converter.md) | The `EqualConverter` is a one way converter that returns a `bool` indicating whether the binding value is equal to another specified value. |
| [`IsListNotNullOrEmptyConverter`](is-list-not-null-or-empty-converter.md) | The `IsListNotNullOrEmptyConverter` is a one way converter that converts `IEnumerable` to a `bool` value. |
| [`IsListNullOrEmptyConverter`](is-list-null-or-empty-converter.md) | The `IsListNullOrEmptyConverter` is a one way converter that converts `IEnumerable` to a `bool` value. |
| [`NotEqualConverter`](not-equal-converter.md) | The `NotEqualConverter` is a one way converter that returns a `bool` indicating whether the binding value is not equal to another specified value. |