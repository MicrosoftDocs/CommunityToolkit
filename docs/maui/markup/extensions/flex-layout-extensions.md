---
title: FlexLayout extensions - .NET MAUI Community Toolkit
author: danielftz
description: The FlexLayout extensions provide a series of extension methods that support positioning Views in FlexLayouts.
ms.date: 04/06/2022
---

# FlexLayout extensions

The FlexLayout extensions provide a series of extension methods that support positioning a `View` in a `FlexLayout`.

The extensions offer the following methods:

## AlignSelf

The `AlignSelf` extension method allows you to set how a `View` in `FlexLayout` is aligned on the cross axis. Setting this property overrides the `AlignItems` property set on the parent `FlexLayout` itself. For further detail refer to the [Microsoft documentation](/dotnet/maui/user-interface/layouts/layouts/flexlayout#alignself).

The following example sets the `AlignSelfProperty` for a `Label` to `FlexAlignSelf.Stretch`:

```cs
new Label().AlignSelf(FlexAlignSelf.Stretch);
```

## Basis

The `Basis` extension method allows you to set the amount of space that's allocated to a `View` in `FlexLayout` on the main axis. The size can be specified in device-independent units, as a percentage of the size of the `FlexLayout` or based on the `View`'s requested width or height. For further detail refer to the [Microsoft documentation](/dotnet/maui/user-interface/layouts/flexlayout#basis).

The following example sets the `BasisProperty` for a `Label` to `new FlexBasis(50)`

```cs
new Label().Basis(50);
```

There is an additional overload for `Basis` that accepts both `float length` and `bool isRelative`.

The following example sets the `BasisProperty` for a `Label` to `new FlexBasis(50, true)`:

```cs
new Label().Basis(50, true);
```

## Grow

The `Grow` extension method specifies the amount of available space a `View` in `FlexLayout` should use on the main axis. For further detail refer to the [Microsoft documentation](/dotnet/maui/user-interface/layouts/flexlayout#grow).

The following example sets the `GrowProperty` for a `Label` to `1f`

```cs
new Label().Grow(1f);
```

## Order

The `Order` extension method allows you to change the order that the children of the FlexLayout are arranged.  Setting this property overrides the order that it appears in the `Children` collection. For further detail refer to the [Microsoft documentation](/dotnet/maui/user-interface/layouts/flexlayout#order).

The following example sets the `OrderProperty` for a `Label` to `1`

```cs
new Label().Order(1);
```

## Shrink

The `Shrink` extension method allows you to indicate which `View` in `FlexLayout` is given priority in being displayed at their full sizes when the aggregate size of `Children` is greater than 
on the main axis. For further detail refer to the [Microsoft documentation](/dotnet/maui/user-interface/layouts/flexlayout#shrink).

The following example sets the `ShrinkProperty` for a `Label` to `0f`

```cs
new Label().Shrink(0f);
```

## API

You can find the source code for the `FlexLayout` extension methods over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui.Markup/blob/main/src/CommunityToolkit.Maui.Markup/FlexLayoutExtensions.cs).