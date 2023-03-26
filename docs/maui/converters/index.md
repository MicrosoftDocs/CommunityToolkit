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
| [`BoolToObjectConverter`](bool-to-object-converter.md) | The `BoolToObjectConverter` is a converter that allows users to convert a `bool` value binding to a specific object. |
| [`ByteArrayToImageSourceConverter`](byte-array-to-image-source-converter.md) | The `ByteArrayToImageSourceConverter` is a converter that allows the user to convert an incoming value from a `byte` array and returns an `ImageSource`. |
| [`ColorToBlackOrWhiteConverter`](color-to-black-or-white-converter.md) | The `ColorToBlackOrWhiteConverter` is a one-way converter that allows users to convert an incoming `Color` to a monochrome value of either `Colors.Black` or `Colors.White`. |
| [`ColorToByteAlphaConverter`](color-to-byte-alpha-converter.md) | The `ColorToByteAlphaConverter` is a one-way converter that allows users to convert an incoming `Color` to the **alpha** component as a value between 0 and 255. |
| [`ColorToByteBlueConverter`](color-to-byte-blue-converter.md) | The `ColorToByteBlueConverter` is a one-way converter that allows users to convert an incoming `Color` to the **blue** component as a value between 0 and 255. |
| [`ColorToByteGreenConverter`](color-to-byte-green-converter.md) | The `ColorToByteGreenConverter` is a one-way converter that allows users to convert an incoming `Color` to the **green** component as a value between 0 and 255. |
| [`ColorToByteRedConverter`](color-to-byte-red-converter.md) | The `ColorToByteRedConverter` is a one-way converter that allows users to convert an incoming `Color` to the **red** component as a value between 0 and 255. |
| [`ColorToCmykStringConverter`](color-to-cmyk-string-converter.md) | The `ColorToCmykStringConverter` is a one-way converter that allows users to convert a `Color` value binding to its CMYK `string` equivalent. |
| [`ColorToCmykaStringConverter`](color-to-cmyka-string-converter.md) | The `ColorToCmykaStringConverter` is a one-way converter that allows users to convert a `Color` value binding to its CMYKA `string` equivalent. |
| [`ColorToColorForTextConverter`](color-to-color-for-text-converter.md) | The `ColorToColorForTextConverter` is a one-way converter that allows users to convert an incoming `Color` to a monochrome value of either `Colors.Black` or `Colors.White` based on whether it is determined as being dark for the human eye. |
| [`ColorToDegreeHueConverter`](color-to-degree-hue-converter.md) | The `ColorToDegreeHueConverter` is a one-way converter that allows users to convert an incoming `Color` to the **hue** component as a value between 0 and 360. |
| [`ColorToGrayScaleColorConverter`](color-to-gray-scale-color-converter.md) | The `ColorToGrayScaleColorConverter` is a one-way converter that allows users to convert an incoming `Color` to a grayscale `Color`. |
| [`ColorToHexRgbStringConverter`](color-to-hex-rgb-string-converter.md) | The `ColorToHexRgbStringConverter` is a that allows users to convert a `Color` value binding to its RGB hexadecimal `string` equivalent. |
| [`ColorToHexRgbaStringConverter`](color-to-hex-rgba-string-converter.md) | The `ColorToHexRgbaStringConverter` is a that allows users to convert a `Color` value binding to its RGBA hexadecimal `string` equivalent. |
| [`ColorToHslStringConverter`](color-to-hsl-string-converter.md) | The `ColorToHslStringConverter` is a one-way converter that allows users to convert a `Color` value binding to its HSL `string` equivalent. |
| [`ColorToHslaStringConverter`](color-to-hsla-string-converter.md) | The `ColorToHslaStringConverter` is a one-way converter that allows users to convert a `Color` value binding to its HSLA `string` equivalent. |
| [`ColorToInverseColorConverter`](color-to-inverse-color-converter.md) | The `ColorToInverseColorConverter` is a one-way converter that allows users to convert an incoming `Color` to its inverse. |
| [`ColorToPercentBlackKeyConverter`](color-to-percent-black-key-converter.md) | The `ColorToPercentBlackKeyConverter` is a one-way converter that allows users to convert an incoming `Color` to the **key** component as a value between 0 and 1. |
| [`ColorToPercentCyanConverter`](color-to-percent-cyan-converter.md) | The `ColorToPercentCyanConverter` is a one-way converter that allows users to convert an incoming `Color` to the **cyan** component as a value between 0 and 1. |
| [`ColorToPercentMagentaConverter`](color-to-percent-magenta-converter.md) | The `ColorToPercentMagentaConverter` is a one-way converter that allows users to convert an incoming `Color` to the **magenta** component as a value between 0 and 1. |
| [`ColorToPercentYellowConverter`](color-to-percent-yellow-converter.md) | The `ColorToPercentYellowConverter` is a one-way converter that allows users to convert an incoming `Color` to the **yellow** component as a value between 0 and 1. |
| [`ColorToRgbStringConverter`](color-to-rgb-string-converter.md) | The `ColorToRgbStringConverter` is a one-way converter that allows users to convert a `Color` value binding to its RGB `string` equivalent. |
| [`ColorToRgbaStringConverter`](color-to-rgba-string-converter.md) | The `ColorToRgbaStringConverter` is a one-way converter that allows users to convert a `Color` value binding to its RGBA `string` equivalent. |
| [`CompareConverter`](compare-converter.md) | The `CompareConverter` is a one-way converter that take an incoming value implementing `IComparable`, compares to a specified value, and returns the comparison result. |
| [`DateTimeOffsetConverter`](datetimeoffsetconverter.md) | The `DateTimeOffsetConverter` is a converter that allows users to convert a `DateTimeOffset` to a `DateTime` |
| [`DoubleToIntConverter`](double-to-int-converter.md) | The `DoubleToIntConverter` is a converter that allows users to convert an incoming `double` value to an `int` and vice-versa. Optionally the user can provide a multiplier to the conversion through the `Ratio` property. |
| [`EnumToBoolConverter`](enum-to-bool-converter.md) | The `EnumToBoolConverter` is a one-way converter that allows you to convert an `Enum` to a corresponding `bool` based on whether it is equal to a set of supplied enum values. It is useful when binding a collection of values representing an enumeration type to a boolean control property like the `IsVisible` property. |
| [`EnumToIntConverter`](enum-to-int-converter.md) | The `EnumToIntConverter` is a converter that allows you to convert a standard `Enum` (extending int) to its underlying primitive `int` type. It is useful when binding a collection of values representing an enumeration type with default numbering to a control such as a `Picker`. |
| [`ImageResourceConverter`](image-resource-converter.md) | The `ImageResourceConverter` is a converter that converts embedded image resource ID to its ImageSource. |
| [`IndexToArrayItemConverter`](index-to-array-item-converter.md) | The `IndexToArrayItemConverter` is a converter that allows users to convert an `int` value binding to an item in an array. The `int` value being data bound represents the indexer used to access the array. The array is passed in through the `ConverterParameter`. |
| [`IntToBoolConverter`](int-to-bool-converter.md) | The `IntToBoolConverter` is a converter that allows users to convert an incoming `int` value to a `bool` and vice-versa. |
| [`InvertedBoolConverter`](inverted-bool-converter.md) | The `InvertedBoolConverter` is a converter that allows users to convert a `bool` to its inverse - `true` becomes `false` and vice-versa. |
| [`IsEqualConverter`](is-equal-converter.md) | The `IsEqualConverter` is a one-way converter that returns a `bool` indicating whether the binding value is equal to another specified value. |
| [`IsInRangeConverter`](is-in-range-converter.md) | The `IsInRangeConverter` is a one-way converter that takes an incoming value implementing `IComparable`, and a minimum and maximum value, and returns the result of the value being between the minimum and maximum values.
| [`IsListNotNullOrEmptyConverter`](is-list-not-null-or-empty-converter.md) | The `IsListNotNullOrEmptyConverter` is a one-way converter that converts `IEnumerable` to a `bool` value. |
| [`IsListNullOrEmptyConverter`](is-list-null-or-empty-converter.md) | The `IsListNullOrEmptyConverter` is a one-way converter that converts `IEnumerable` to a `bool` value. |
| [`IsNotEqualConverter`](is-not-equal-converter.md) | The `IsNotEqualConverter` is a one-way converter that returns a `bool` indicating whether the binding value is not equal to another specified value. |
| [`IsNullConverter`](is-null-converter.md) | The `IsNullConverter` is a converter that allows users to convert an incoming binding to a `bool` value. This value represents if the incoming binding value is null. |
| [`IsNotNullConverter`](is-not-null-converter.md) | The `IsNotNullConverter` is a converter that allows users to convert an incoming binding to a `bool` value. This value represents if the incoming binding value is not null. |
| [`IsStringNotNullOrEmptyConverter`](is-string-not-null-or-empty-converter.md) | The `IsStringNotNullOrEmptyConverter` is a one-way converter that returns a `bool` indicating whether the binding value is not null and not an `string.Empty`. |
| [`IsStringNotNullOrWhiteSpaceConverter`](is-string-not-null-or-whitespace-converter.md) | The `IsStringNotNullOrWhiteSpaceConverter` is a one-way converter that returns a `bool` indicating whether the binding value is not null, not an `string.Empty` and does not contain whitespace characters only. |
| [`IsStringNullOrEmptyConverter`](is-string-null-or-empty-converter.md) | The `IsStringNullOrEmptyConverter` is a one-way converter that returns a `bool` indicating whether the binding value is null or `string.Empty`. |
| [`IsStringNullOrWhiteSpaceConverter`](is-string-null-or-whitespace-converter.md) | The `IsStringNullOrWhiteSpaceConverter` is a one-way converter that returns a `bool` indicating whether the binding value is null, `string.Empty` or contains whitespace characters only. |
| [`ItemTappedEventArgsConverter`](item-tapped-eventargs-converter.md) | The `ItemTappedEventArgsConverter` is a converter that allows users to extract the Item value from an `ItemTappedEventArgs` object. It can subsequently be used in combination with [EventToCommandBehavior](../behaviors/event-to-command-behavior.md). |
| [`ListToStringConverter`](list-to-string-converter.md) | The `ListToStringConverter` is a one-way converter that returns a concatenation of the members of a collection, using the specified separator between each member. |
| [`MathExpressionConverter`](math-expression-converter.md) | The `MathExpressionConverter` is a converter that allows users to perform various math operations. |
| [`MultiConverter`](multi-converter.md) | The `MultiConverter` converts an incoming value using all of the incoming converters in sequence. |
| [`MultiMathExpressionConverter`](multi-math-expression-converter.md) | The `MultiMathExpressionConverter` is a converter that allows users to perform various math operations with multiple values through using a `MultiBinding`. |
| [`SelectedItemEventArgsConverter`](selected-item-eventargs-converter.md) | The `SelectedItemEventArgsConverter` is a converter that allows users to extract the Item value from an `SelectedItemEventArgs` object. It can subsequently be used in combination with [EventToCommandBehavior](../behaviors/event-to-command-behavior.md). |
| [`StateToBoolConverter`](state-to-bool-converter.md) | The `StateToBoolConverter` is a one-way converter that returns a `boolean` result based on whether the supplied value is of a specific `LayoutState`. |
| [`StringToListConverter`](string-to-list-converter.md) | The `StringToListConverter` is a one-way converter that returns a set of substrings by splitting the input string based on one or more separators. |
| [`TextCaseConverter`](text-case-converter.md) | The `TextCaseConverter` is a one-way converter that allows users to convert the casing of an incoming `string` type binding. The `Type` property is used to define what kind of casing will be applied to the string. |
| [`VariableMultiValueConverter`](variable-multi-value-converter.md) | The `VariableMultiValueConverter` is a converter that allows users to convert `bool` values via a `MultiBinding` to a single `bool`. |
