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

#### One way binding

A one way binding from a view model (`RegistrationViewModel`) property called `RegistrationCode` to the `Text` property of an `Label` can be created as follows:

```csharp
new Entry().Bind(Label.TextProperty, static (RegistrationViewModel vm) => vm.RegistrationCode)
```

#### Two way binding

A two way binding from a view model (`RegistrationViewModel`) property called `RegistrationCode` to the `Text` property of an `Entry` can be created as follows:

```csharp
new Entry().Bind(
    Entry.TextProperty,
    static (RegistrationViewModel vm) => vm.RegistrationCode,
    static (RegistrationViewModel vm, string code) => vm.RegistrationCode = code)
```

#### Default property

The `Bind` method can be called without specifying the property to set the binding up for, this will utilize the defaults provided by the library with the full list at the [GitHub repository](https://github.com/CommunityToolkit/Maui.Markup/blob/523ff96160889f0806f7686e25c5d651fa7d8b7e/src/CommunityToolkit.Maui.Markup/DefaultBindableProperties.cs).

The default property to bind for an `Entry` is the text property. So the above example could be written as:

```csharp
new Entry().Bind(nameof(ViewModel.RegistrationCode))
```

> [!WARNING]
> This approach will result in some level of Reflection being used and will not perform as well as the [Explicit property](#inline-conversion) approach.

#### Value conversion

The `Bind` method allows for a developer to supply the `Converter` that they wish to use in the binding or simply provide a mechanism to use an inline conversion.

##### Converter

```csharp
new Entry()
    .Bind(
        Entry.TextProperty,
        static (RegistrationViewModel vm) => vm.RegistrationCode,
        converter: new TextCaseConverter { Type = TextCaseType.Upper });
```

> [!WARNING]
> This approach will result in some level of Reflection being used and will not perform as well as the [Explicit property](#inline-conversion) approach.

See [`TextCaseConverter`](../../converters/text-case-converter.md) for the documentation on it's full usage.

##### Inline conversion

```csharp
new Entry()
    .Bind(
        Entry.TextProperty,
        static (RegistrationViewModel vm) => vm.RegistrationCode,
        convert: (string? text) => text?.ToUpperInvariant());
```

#### Multiple Bindings

Multiple Bindings can be aggregated together leveraging the `IMultiValueConverter`.

The `convert` parameter is a `Func` that is required to convert the multiple bindings to the required result.

```csharp
new Label()
    .Bind(
        Label.TextProperty,
        binding1: new Binding(nameof(ViewModel.IsBusy)),
        binding2: new Binding(nameof(ViewModel.LabelText)),
        convert: ((bool IsBusy, string LabelText) values) => values.IsBusy ? string.Empty : values.LabelText)
```

## BindCommand

The `BindCommand` method provides a helpful way of configuring a binding to a default provided by the library with the full list at the [GitHub repository](https://github.com/CommunityToolkit/Maui.Markup/blob/523ff96160889f0806f7686e25c5d651fa7d8b7e/src/CommunityToolkit.Maui.Markup/DefaultBindableProperties.cs).

The default command to bind for an `Button` is the `Command` property. So the following example sets up a binding to that property.

```csharp
new Button().BindCommand(static (ViewModel vm) => vm.SubmitCommand);
```

The above could also be written as:

> [!NOTE]
> If the default command does not result in binding to your desired command then you can use the `Bind` method.

```csharp
new Button()
    .Bind(
        Entry.CommandProperty,
        static (RegistrationViewModel vm) => vm.SubmitCommand,
        mode: BindingMode.OneTime);
```

## AppThemeBinding

The `AppThemeBinding` method allows for a light and dark value to assigned to a `BindableProperty` so that when the applications `AppTheme` is modified the appropriate value will be used for that theme.

The following example will assign the color black to the `Text` property of the `Label` control if the application is running in light theme and white in dark theme.

```csharp
new Label().AppThemeBinding(Label.TextColorProperty, Colors.Black, Colors.White);
```

> [!NOTE]
> There is a more specific method when dealing with `Color` properties. `AppThemeColorBinding` will perform the same underlying behavior as `AppThemeBinding` but it requires a set of `Color` parameters.

For more information refer to the [Theming](../theming.md) documentation.

## Examples

You can find an example of these extension methods in action throughout the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui.Markup/blob/main/samples/CommunityToolkit.Maui.Markup.Sample/).

## API

You can find the source code for the `BindableObject` extension methods over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui.Markup/blob/main/src/CommunityToolkit.Maui.Markup/BindableObjectExtensions.cs).
