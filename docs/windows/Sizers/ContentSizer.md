---
title: ContentSizer
author: michael-hawker
description: The ContentSizer is a control which can be used to resize any element, usually its parent.
keywords: ContentSizer, SizerBase, Control, Layout, Expander, Splitter
dev_langs:
  - csharp
category: Controls
subcategory: Sizers
discussion-id: 96
issue-id: 101
icon: Assets/ContentSizer.png
---

# ContentSizer

If you are using a `Grid`, use [GridSplitter](GridSplitter.md) instead.

The main use-case for a ContentSizer is to create an expandable shelf for your application. This allows the `Expander` itself to remember its opening/closing sizes.

A GridSplitter would be insufficient as it would force the grid to remember the row size and maintain its position when the `Expander` collapses.

:::code language="xaml" source="~/../code-windows/components/Sizers/samples/ContentSizerTopShelfPage.xaml":::

:::code language="csharp" source="~/../code-windows/components/Sizers/samples/ContentSizerTopShelfPage.xaml.cs":::The following example shows how to use the ContentSizer to create a left-side shelf; however, this scenario can also be accomplished with a `GridSplitter`.

:::code language="xaml" source="~/../code-windows/components/Sizers/samples/ContentSizerLeftShelfPage.xaml":::

:::code language="csharp" source="~/../code-windows/components/Sizers/samples/ContentSizerLeftShelfPage.xaml.cs":::
