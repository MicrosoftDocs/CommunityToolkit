---
title: BindableObject extensions - .NET MAUI Community Toolkit
author: bijington
description: The BindableObject extensions provide a series of extension methods that support configuring Bindings on a BindableObject.
ms.date: 03/27/2022
---

# BindableObject extensions

The `BindableObject` extensions provide a series of extension methods that support configuring `Binding`s on a `BindableObject`.

The extensions offer the following methods:

## Bind

The `Bind` method offers a number of overloads providing different convenience around the setup of a `Binding`. For further information of the possibilities of `Binding` data in a .NET MAUI application refer to the [Microsoft documentation](/dotnet/maui/fundamentals/data-binding/).

### Example

There are a number of overloads for the `Bind` method.

#### Explicit Property

A binding from a view model property called `RegistrationCode` to the text property of an `Entry` can be created as follows:

```csharp
new Entry().Bind(Entry.TextProperty, nameof(ViewModel.RegistrationCode))
```

#### Default Property

`Bind` can be called without specifying the property to set the binding up for, this will utilise the defaults provided by the library with the full list at the [GitHub repository](https://github.com/CommunityToolkit/Maui.Markup/blob/523ff96160889f0806f7686e25c5d651fa7d8b7e/src/CommunityToolkit.Maui.Markup/DefaultBindableProperties.cs). 

The default property to bind for an `Entry` is the text property. So the above example could be written as:

```csharp
new Entry().Bind(nameof(ViewModel.RegistrationCode))
```

#### Value conversion

The `Bind` allows for a developer to supply the `Converter` that they wish to use in the binding or simply provide a mechanism to use an inline conversion.

##### Converter

```csharp
new Entry()
    .Bind(
        nameof(ViewModel.RegistrationCode),
        converter: new TextCaseConverter { Type = TextCaseType.Upper });
```

See [`TextCaseConverter`](../../converters/text-case-converter.md) for the documentation on it's full usage.

##### Inline conversion

```csharp
new Entry()
    .Bind(
        nameof(ViewModel.RegistrationCode),
        convert: (string? text) => text?.ToUpperInvariant());
```

## BindCommand

## Assign

The `Assign` method makes it possible to refer to the `BindableObject` being fluently built within the calls. This is extremly useful for setting up a `RelativeSource` to `Self` binding.

This example binds the `TextColor` of the `Label` to inverse of it's `BackgroundColor`:

```csharp
Content = new Label()
    .Assign(out var self)
    .Bind(
        Label.TextColorProperty,
        path: nameof(Label.BackgroundColor),
        source: self,
        converter: new ColorToInverseColorConverter());
```

## Invoke