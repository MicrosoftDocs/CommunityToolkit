---
title: FuncConverter - .NET MAUI Community Toolkit
author: bijington
description: The FuncConverter provides the ability to define an IValueConverter implementation inline when build your UI.
ms.date: 05/22/2022
---

# FuncConverter

The `FuncConverter` provides the ability to define an `IValueConverter` implementation inline when build your UI. An additional benefit of using the `FuncConverter` implementation is that it provides a type safe way of performing your conversions. The C# Markup package uses the `FuncConverter` internally for the [inline conversion option](../extensions/bindable-object-extensions.md#inline-conversion) in the `Bind` extension method.

> [!NOTE]
> `FuncConverter` only supports a single `Binding` value, if you required `MultiBinding` support refer to [`FuncMultiConverter`](func-multi-converter.md).

The converter offers many different ways of defining your conversion based on how much information is required.

## FuncConverter&lt;TSource>

The `FuncConverter<TSource>` implementation allows you to define a conversion process that provides **only** a type safe incoming value.

The following example shows how to build a converter that will convert between a `TimeSpan` and a `double` expressed in seconds:

```csharp
var converter = new FuncConverter<TimeSpan>(
    convert: (time) => time.TotalSeconds,
    convertBack: (value) => TimeSpan.FromSeconds((double)value));
```

Both the `convert` and `convertBack` parameters are optional to allow developers to define only what is required.

You will notice that the the `convertBack` method does not appear type safe here.

## FuncConverter&lt;TSource, TDest>

The `FuncConverter<TSource, TDest>` implementation allows you to define a conversion process that provides a type safe incoming value and a type safe return value.

Using the same example as above we can make the `convertBack` implementation type safe and easier to read:

```csharp
var converter = new FuncConverter<TimeSpan, double>(
    convert: (time) => time.TotalSeconds,
    convertBack: (seconds) => TimeSpan.FromSeconds(seconds));
```

Both the `convert` and `convertBack` parameters are optional to allow developers to define only what is required.

## FuncConverter&lt;TSource, TDest, TParam>

The `FuncConverter<TSource, TDest, TParam>` implementation allows you to define a conversion process that provides a type safe incoming value, a type safe return value and a type safe `ConverterParameter`.

Using the same example as above we can include the `ConverterParameter` from the `Binding`:

```csharp
var converter = new FuncConverter<TimeSpan, double, int>(
    convert: (time, offset) => time.TotalSeconds + offset,
    convertBack: (seconds, offset) => TimeSpan.FromSeconds(seconds - offset));
```

Both the `convert` and `convertBack` parameters are optional to allow developers to define only what is required.

## API

You can find the source code for the `FuncConverter` feature over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui.Markup/blob/main/src/CommunityToolkit.Maui.Markup/FuncConverter.cs).
