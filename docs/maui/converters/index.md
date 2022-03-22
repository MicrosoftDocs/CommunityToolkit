---
title: Converters - .NET MAUI Community Toolkit
author: bijington
description: The .NET MAUI Community Toolkit provides a collection of pre-built, reusable converters to make developers lives easier.
ms.date: 03/13/2022
---

# Converters

.NET Multi-platform App UI (.NET MAUI) data bindings usually transfer data from a source property to a target property, and in some cases from the target property to the source property. This transfer is straightforward when the source and target properties are of the same type, or when one type can be converted to the other type through an implicit conversion. When that is not the case, a type conversion must take place.

For further information on Converters please refer to the [.NET MAUI documentation](/dotnet/maui/fundamentals/data-binding/converters).

## .NET MAUI Community Toolkit Converters

The .NET MAUI Community Toolkit provides a collection of pre-built, reusable converters to make developers lives easier. Here are the converters provided by the toolkit:

| Converter | Description |
| --------- | ----------- |
| [`DoubleToIntConverter`](double-to-int-converter.md) | The `DoubleToIntConverter` is a converter that allows users to convert an incoming `double` value to an `int` and vice-versa. Optionally the user can provide a multiplier to the conversion through the `Ratio` property. |
| [`EqualConverter`](equal-converter.md) | The `EqualConverter` is a one way converter that returns a `bool` indicating whether the binding value is equal to another specified value. |
| [`IntToBoolConverter`](int-to-bool-converter.md) | The `IntToBoolConverter` is a converter that allows users to convert an incoming `int` value to a `bool` and vice-versa. |
| [`InvertedBoolConverter`](inverted-bool-converter.md) | The `InvertedBoolConverter` is a converter that allows users to convert a `bool` to its inverse - `true` becomes `false` and vice-versa. |
| [`IsListNotNullOrEmptyConverter`](is-list-not-null-or-empty-converter.md) | The `IsListNotNullOrEmptyConverter` is a one way converter that converts `IEnumerable` to a `bool` value. |
| [`IsListNullOrEmptyConverter`](is-list-null-or-empty-converter.md) | The `IsListNullOrEmptyConverter` is a one way converter that converts `IEnumerable` to a `bool` value. |
| [`NotEqualConverter`](not-equal-converter.md) | The `NotEqualConverter` is a one way converter that returns a `bool` indicating whether the binding value is not equal to another specified value. |
| [`TextCaseConverter`](text-case-converter.md) | The `TextCaseConverter` is a one way converter that allows users to convert the casing of an incoming `string` type binding. The `Type` property is used to define what kind of casing will be applied to the string. |
| [`DateTimeOffsetConverter`](datetimeoffsetconverter.md) | The `DateTimeOffsetConverter` is a converter that allows users to convert a `DateTimeOffset` to a `DateTime`
| [`EnumToIntConverter`](enumtointconverter.md) | The `EnumToIntConverter` is a converter that allows you to convert a standard `Enum` (extending int) to its underlying primitive `int` type.
