---
title: StaggeredLayout / StaggeredPanel
author: skendrot
description: The StaggeredLayout and StaggeredPanel display items in a column approach where an item will be added to whichever column has used the least amount of space.
keywords: StaggeredPanel, StaggeredLayout, Layout
dev_langs:
  - csharp
category: Layouts
subcategory: Panel
discussion-id: 0
issue-id: 0
icon: Assets/StaggeredPanel.png
---

# StaggeredLayout / StaggeredPanel

## StaggeredLayout

The `StaggeredLayout` allows for layout of items in a column approach where an item will be added to whichever column has used the least amount of space.

It is a Layout for `ItemsRepeater` which will provide better virtualization compared to the `StaggeredPanel` below.

:::code language="xaml" source="~/../code-windows/components/Primitives/samples/StaggeredLayoutSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Primitives/samples/StaggeredLayoutSample.xaml.cs":::

## StaggeredPanel

The `StaggeredPanel` allows for layout of items in a column approach where an item will be added to whichever column has used the least amount of space.

```xaml
<ItemsControl>
    <ItemsControl.ItemTemplate>
        <DataTemplate>
            <Image Source="{Binding Thumbnail}"/>
        </DataTemplate>
    </ItemsControl.ItemTemplate>
    <ItemsControl.ItemsPanel>
        <ItemsPanelTemplate>
            <controls:StaggeredPanel/>
        </ItemsPanelTemplate>
    </ItemsControl.ItemsPanel>
</ItemsControl>
```

