---
title: FuncMultiConverter - .NET MAUI Community Toolkit
author: bijington
description: The FuncMultiConverter provides the ability to define an IMultiValueConverter implementation inline when build your UI.
ms.date: 05/22/2022
---

# FuncMultiConverter

The `FuncMultiConverter` provides the ability to define an `IMultiValueConverter` implementation inline when build your UI. An additional benefit of using the `FuncMultiConverter` implementation is that it provides a type safe way of performing your conversions. The C# Markup package uses the `FuncMultiConverter` internally for the [multiple bindings option](../extensions/bindable-object-extensions.md#multiple-bindings) in the `Bind` extension method.

> [!NOTE]
> `FuncMultiConverter` only supports a `MultiBinding`, if you required `Binding` support refer to [`MultiConverter`](func-converter.md).

The converter offers many different ways of defining your conversion based on how much information is required.

## FuncMultiConverter&lt;TSource1, TSource2, TDest>

The `FuncMultiConverter<TSource1, TSource2, TDest>` implementation allows you to define a conversion process that provides type safe incoming values and a type safe return value. This implementation expects **exactly 2** incoming values.

The following example shows how to build a converter that will convert 2 incoming `string`s in to a semi-colon separated `string`:

```csharp
var converter = new FuncMultiConverter<string, string, string>(
    convert: ((string First, string Second) lines) => string.Join(';', lines.First, lines.Second),
    convertBack: (text) =>
    {
        var lines = text.Split(';');

        return (lines[0], lines[1]);
    });
```

Both the `convert` and `convertBack` parameters are optional to allow developers to define only what is required.

> [!NOTE]
> `FuncMultiConverter` supports up to 4 typed incoming values.

## FuncMultiConverter&lt;TSource1, TSource2, TDest, TParam>

The `FuncMultiConverter<TSource1, TSource2, TDest>` implementation allows you to define a conversion process that provides type safe incoming values, a type safe return value and a type safe `ConverterParameter`. This implementation expects **exactly 2** incoming values.

The following example shows how to build a converter that will convert 2 incoming `string`s in to a character supplied by the `ConverterParameter` separated `string`:

```csharp
var converter = new FuncMultiConverter<string, string, string, char>(
    convert: ((string First, string Second) lines, char separator) => string.Join(separator, lines.First, lines.Second),
    convertBack: (text, char separator) =>
    {
        var lines = text.Split(separator);

        return (lines[0], lines[1]);
    });
```

Both the `convert` and `convertBack` parameters are optional to allow developers to define only what is required.

## API

You can find the source code for the `FuncMultiConverter` feature over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui.Markup/blob/main/src/CommunityToolkit.Maui.Markup/FuncMultiConverter.cs).
