---
title: .NET MAUI Community Toolkit - Markup
author: bijington
description: C# Markup is a set of fluent helper methods and classes designed to simplify the process of building declarative .NET Multi-platform App UI (.NET MAUI) user interfaces in code.
ms.date: 02/13/2022
---

# C# Markup

## Overview

C# Markup is a set of fluent helper methods and classes designed to simplify the process of building declarative .NET Multi-platform App UI (.NET MAUI) user interfaces in code. The fluent API provided by C# Markup is available in the `CommunityToolkit.Maui.Markup` namespace.

Just as with XAML, C# Markup enables a clean separation between UI (View) and Business Logic (View Model).

C# Markup is available on all platforms supported by .NET MAUI.

## NuGet package

The C# Markup package can be included in your project(s) as described in our [Getting started](../get-started.md) guide.

## Examples

Here are some brief examples showing how common tasks can be achieved through the use of the Markup package.

### Bindings

First let's take a look at how a Binding could be defined without the Markup package:

```csharp
var entry = new Entry();
entry.SetBinding(Entry.TextProperty, new Binding(nameof(ViewModel.RegistrationCode));
```

Markup allows us to define the binding fluently and therefore chain multiple methods together to reduce the verbosity of our code:

```csharp
new Entry().Bind(Entry.TextProperty, static (ViewModel vm) => vm.RegistrationCode, static (ViewModel vm, string text) => vm.RegistrationCode = text)
```

For further details on the possible options for the `Bind` method refer to the [`BindableObject` extensions documentation](extensions/bindable-object-extensions.md).

### Sizing

First let's take a look at how an `Entry` could be sized without the Markup package:

```csharp
var entry = new Entry();
entry.WidthRequest = 200;
entry.HeightRequest = 40;
```

Markup allows us to define the sizing fluently and therefore chain multiple methods together to reduce the verbosity of our code:

```csharp
new Entry().Size(200, 40);
```

For further details on the possible options for the `Size` method refer to the [`VisualElement` extensions documentation](extensions/visual-element-extensions.md).

### In-depth example

This example creates a `Grid` object, with child `Label` and `Entry` objects. The `Label` displays text, and the `Entry` data binds to the `RegistrationCode` property of the viewmodel. Each child view is set to appear in a specific row in the `Grid`, and the `Entry` spans all the columns in the `Grid`. In addition, the height of the `Entry` is set, along with its keyboard, colors, the font size of its text, and its `Margin`. 

C# Markup extensions also allow developers to define names for Columns and Rows (e.g. `Column.Input`) using an `enum`.

C# Markup enables this to be defined using its fluent API:

```csharp
using static CommunityToolkit.Maui.Markup.GridRowsColumns;

class SampleContentPage : ContentPage
{
    public SampleContentPage()
    {
        Content = new Grid
        {
            RowDefinitions = Rows.Define(
                (Row.TextEntry, 36)),

            ColumnDefinitions = Columns.Define(
                (Column.Description, Star),
                (Column.Input, Stars(2))),

            Children =
            {
                new Label()
                    .Text("Code:")
                    .Row(Row.TextEntry).Column(Column.Description),

                new Entry
                {
                    Keyboard = Keyboard.Numeric,
                }.Row(Row.TextEntry).Column(Column.Input)
                 .BackgroundColor(Colors.AliceBlue)
                 .FontSize(15)
                 .Placeholder("Enter number")
                 .TextColor(Colors.Black)
                 .Height(44)
                 .Margin(5, 5)
                 .Bind(Entry.TextProperty, static (ViewModel vm) => vm.RegistrationCode, static (ViewModel vm, string text) => vm.RegistrationCode = text)
            }
        };
    }

    enum Row { TextEntry }
    enum Column { Description, Input }
}
```

## Converters

The C# Markup package provides the ability to define `IValueConverter` and `IMultiValueConverter` implementations inline when building your applications UI.

| Converter | Description |
| --------- | ----------- |
| [`FuncConverter`](converters/func-converter.md) | The `FuncConverter` provides the ability to define an `IValueConverter` implementation inline when build your UI. |
| [`FuncMultiConverter`](converters/func-multi-converter.md) | The `FuncMultiConverter` provides the ability to define an `IMultiValueConverter` implementation inline when build your UI. |

## Extensions

> [!NOTE]
> C# Markup includes extension methods that set specific view properties. They are designed to improve code readability, and can be used in combination with property setters. It's recommended to always use an extension method when one exists for a property, but you can choose your preferred balance.

| Extension | Description |
| --------- | ----------- |
| [`AbsoluteLayout`](extensions/absolute-layout-extensions.md) | The AbsoluteLayout extensions provide a series of extension methods that support positioning `View`s in `AbsoluteLayout`s. |
| [`AutomationProperties`](extensions/automation-properties.md) | The `AutomationProperties` extensions provide a series of extension methods that support the configuring of accessibility related settings. |
| [`BindableLayout`](extensions/bindable-layout-extensions.md) | The `BindableLayout` extensions provide a series of extension methods that support configuring its `EmptyView`, `ItemSource` and `ItemTemplate`. |
| [`BindableObject`](extensions/bindable-object-extensions.md) | The `BindableObject` extensions provide a series of extension methods that support configuring `Binding`s on a `BindableObject`. |
| [`DynamicResourceHandler`](extensions/dynamic-resource-handler-extensions.md) | The `DynamicResourceHandler` extensions provide a series of extension methods that support configuring `IDynamicResourceHandler` which can be used to theme an App. |
| [`Element`](extensions/element-extensions.md) | The `Element` extensions provide a series of extension methods that support configuring the padding, effects, font attributes, dynamic resources, text, and text color of an `Element`. |
| [`FlexLayout`](extensions/flex-layout-extensions.md) | The FlexLayout extensions provide a series of extension methods that support positioning a `View` in a `FlexLayout`. |
| [`Grid`](extensions/grid-extensions.md) | The Grid extensions provide a series of extension methods that support configuring a Grid. |
| [`Image`](extensions/image-extensions.md) | The `Image` extensions provide a series of extension methods that support configuring `IImage` controls. |
| [`ItemsView`](extensions/itemsview-extensions.md) | The `ItemsView` extensions provide a series of extension methods that support configuring `ItemsView` controls such as `CarouselView` and `CollectionView`. |
| [`Label`](extensions/label-extensions.md) | The `Label` extensions provide a series of extension methods that support configuring `Label` controls. |
| [`Placeholder`](extensions/placeholder-extensions.md) | The `Placeholder` extensions provide a series of extension methods that support configuring `IPlaceholder` controls. |
| [`SemanticProperties`](extensions/semantic-properties.md) | The `SemanticProperties` extensions provide a series of extension methods that support the configuring of accessibility related settings. |
| [`Style`](extensions/style.md) | `Style<T>` provides a series of fluent extension methods that support configuring `Microsoft.Maui.Controls.Style`. |
| [`TextAlignment`](extensions/text-alignment-extensions.md) | The `TextAlignment` extensions provide a series of extension methods that support configuring the `HorizontalTextAlignment` and `VeticalTextAlignment` properties on controls implementing `ITextAlignment`. |
| [`View`](extensions/visual-element-extensions.md) | The `View` extensions provide a series of extension methods that support configuring the alignment of controls inheriting from `View`. |
| [`VisualElement`](extensions/visual-element-extensions.md) | The `VisualElement` extensions provide a series of extension methods that support configuring the sizing, styling and behaviors of a `VisualElement`. |
