---
title: Converters - .NET MAUI Community Toolkit
author: bijington
description: The .NET MAUI Community Toolkit provides a collection of pre-built, reusable converters to make developers lives easier.
ms.date: 03/13/2022
---

# Converters

[!INCLUDE [docs under construction](../includes/preview-note.md)]

.NET Multi-platform App UI (.NET MAUI) data bindings usually transfer data from a source property to a target property, and in some cases from the target property to the source property. This transfer is straightforward when the source and target properties are of the same type, or when one type can be converted to the other type through an implicit conversion. When that is not the case, a type conversion must take place.

For further information on Converters please refer to the [.NET MAUI documentation](/dotnet/maui/fundamentals/data-binding/converters).

## .NET MAUI Community Toolkit Converters

The .NET MAUI Community Toolkit provides a collection of pre-built, reusable converters to make developers lives easier. Here are the converters provided by the toolkit:

| Converter | Description |
| --------- | ----------- |
| [`ColorToBlackOrWhiteConverter`](color-to-black-or-white-converter.md) | The `ColorToBlackOrWhiteConverter` is a one way converter that allows users to convert an incoming `Color` to a monochrome value of either `Colors.Black` or `Colors.White`. |
| [`ColorToColorForTextConverter`](color-to-color-for-text-converter.md) | The `ColorToColorForTextConverter` is a one way converter that allows users to convert an incoming `Color` to a monochrome value of either `Colors.Black` or `Colors.White` based on whether it is determined as being dark for the human eye. |
| [`ColorToGrayScaleColorConverter`](color-to-gray-scale-color-converter.md) | The `ColorToGrayScaleColorConverter` is a one way converter that allows users to convert an incoming `Color` to a grayscale `Color`. |
| [`ColorToInverseColorConverter`](color-to-inverse-color-converter.md) | The `ColorToInverseColorConverter` is a one way converter that allows users to convert an incoming `Color` to its inverse. |
| [`DateTimeOffsetConverter`](datetimeoffsetconverter.md) | The `DateTimeOffsetConverter` is a converter that allows users to convert a `DateTimeOffset` to a `DateTime` |
| [`DoubleToIntConverter`](double-to-int-converter.md) | The `DoubleToIntConverter` is a converter that allows users to convert an incoming `double` value to an `int` and vice-versa. Optionally the user can provide a multiplier to the conversion through the `Ratio` property. |
| [`IntToBoolConverter`](int-to-bool-converter.md) | The `IntToBoolConverter` is a converter that allows users to convert an incoming `int` value to a `bool` and vice-versa. |
| [`InvertedBoolConverter`](inverted-bool-converter.md) | The `InvertedBoolConverter` is a converter that allows users to convert a `bool` to its inverse - `true` becomes `false` and vice-versa. |
| [`IsEqualConverter`](is-equal-converter.md) | The `IsEqualConverter` is a one way converter that returns a `bool` indicating whether the binding value is equal to another specified value. |
| [`IsListNotNullOrEmptyConverter`](is-list-not-null-or-empty-converter.md) | The `IsListNotNullOrEmptyConverter` is a one way converter that converts `IEnumerable` to a `bool` value. |
| [`IsListNullOrEmptyConverter`](is-list-null-or-empty-converter.md) | The `IsListNullOrEmptyConverter` is a one way converter that converts `IEnumerable` to a `bool` value. |
| [`IsNotEqualConverter`](is-not-equal-converter.md) | The `IsNotEqualConverter` is a one way converter that returns a `bool` indicating whether the binding value is not equal to another specified value. |
| [`IsStringNotNullOrEmptyConverter`](is-string-not-null-or-empty-converter.md) | The `IsStringNotNullOrEmptyConverter` is a one way converter that returns a `bool` indicating whether the binding value is not null and not an `string.Empty`. |
| [`IsStringNotNullOrWhiteSpaceConverter`](is-string-not-null-or-whitespace-converter.md) | The `IsStringNotNullOrWhiteSpaceConverter` is a one way converter that returns a `bool` indicating whether the binding value is not null, not an `string.Empty` and does not contain whitespace characters only. |
| [`IsStringNullOrEmptyConverter`](is-string-null-or-empty-converter.md) | The `IsStringNullOrEmptyConverter` is a one way converter that returns a `bool` indicating whether the binding value is null or `string.Empty`. |
| [`IsStringNullOrWhiteSpaceConverter`](is-string-null-or-whitespace-converter.md) | The `IsStringNullOrWhiteSpaceConverter` is a one way converter that returns a `bool` indicating whether the binding value is null, `string.Empty` or contains whitespace characters only. |
| [`ItemTappedEventArgsConverter`](itemtappedeventargsconverter.md) | The `ItemTappedEventArgsConverter` is a converter that allows users to extract the Item value from an `ItemTappedEventArgs` object. |
| [`ListToStringConverter`](list-to-string-converter.md) | The `ListToStringConverter` is a one way converter that returns a concatenation of the members of a collection, using the specified separator between each member. |
| [`StringToListConverter`](string-to-list-converter.md) | The `StringToListConverter` is a one way converter that returns a set of substrings by splitting the input string based on one or more separators. |
| [`TextCaseConverter`](text-case-converter.md) | The `TextCaseConverter` is a one way converter that allows users to convert the casing of an incoming `string` type binding. The `Type` property is used to define what kind of casing will be applied to the string. |