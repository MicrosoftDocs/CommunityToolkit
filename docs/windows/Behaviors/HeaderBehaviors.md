---
title: Header Behaviors
author: michael-hawker
description: Behaviors for modifying an element's movement/response when scrolling within a ScrollViewer.
keywords: Behaviors
dev_langs:
  - csharp
category: Xaml
subcategory: Behaviors
discussion-id: 0
issue-id: 0
icon: Assets/HeaderBehaviors.png
---

# Header Behaviors

The `FadeHeaderBehavior`, `QuickReturnHeaderBehavior`, and `StickyHeaderBehavior` most commonly apply behaviors to `ListView`, `GridView`, `HeaderedItemsControl`, and `HeaderedTreeView` elements in their `Header`. It can also be applied to any element contained at the top of a `ScrollViewer`.

They use composition animations to allow the visual of an element of a scrolling viewport to be manipulated for various effects.

> [!WARNING]
> Due to the use of the composition APIs, these behaviors aren't supported on Uno Platform.

To use the behavior, place it on the _element in the header to be manipulated_.

> [!NOTE]
> This is different in 8.x than it was in 7.x where the behavior was placed on the parent containing element (e.g. `ListView`).
> This change was made to enable more scenarios for these components.

## FadeHeaderBehavior

The FadeHeaderBehavior causes the element in the scrolling collection to fade in and out as the user scrolls at the top of the collection.

:::code language="xaml" source="~/../code-windows/components/Behaviors/samples/Headers/FadeHeaderBehaviorSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Behaviors/samples/Headers/FadeHeaderBehaviorSample.xaml.cs":::

## QuickReturnBehavior

The QuickReturnHeaderBehavior causes the element in the scrolling collection to return back into view as soon as the user scrolls up even if they are not near the top of the collection.

:::code language="xaml" source="~/../code-windows/components/Behaviors/samples/Headers/QuickReturnHeaderBehaviorSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Behaviors/samples/Headers/QuickReturnHeaderBehaviorSample.xaml.cs":::

It can also be used to have content quickly re-appear in any `ScrollViewer`:

:::code language="xaml" source="~/../code-windows/components/Behaviors/samples/Headers/QuickReturnScrollViewerSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Behaviors/samples/Headers/QuickReturnScrollViewerSample.xaml.cs":::

## StickyHeaderBehavior

The StickyHeaderBehavior causes the element in the scrolling collection to stay in view as the user scrolls up and down in the collection.

:::code language="xaml" source="~/../code-windows/components/Behaviors/samples/Headers/StickyHeaderBehaviorSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Behaviors/samples/Headers/StickyHeaderBehaviorSample.xaml.cs":::

Or similarly, it can be used with a `HeaderedItemsControl` to maintain context at the top:

:::code language="xaml" source="~/../code-windows/components/Behaviors/samples/Headers/StickyHeaderItemsControlSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Behaviors/samples/Headers/StickyHeaderItemsControlSample.xaml.cs":::


