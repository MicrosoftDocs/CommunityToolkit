---
title: HeaderedContentControl
author: skendrot
description: The HeaderedContentControl allows content to be displayed with a specified header.
keywords: HeaderedContentControl, Control, headered
dev_langs:
  - csharp
category: Controls
subcategory: Layout
discussion-id: 0
issue-id: 0
icon: Assets/HeaderedContentControl.png
---

# HeaderedContentControl

The `Header` property can be any object and you can use the `HeaderTemplate` to specify a custom look to the header. Content for the HeaderedContentControl will align to the top left. This is to maintain the same functionality as the ContentControl.

> [!NOTE]
> Setting the `Background`, `BorderBrush` and `BorderThickness` properties will not have any effect on the HeaderedContentControl. This is to maintain the same functionality as the ContentControl.

:::code language="xaml" source="~/../code-windows/components/HeaderedControls/samples/HeaderedContentControlSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/HeaderedControls/samples/HeaderedContentControlSample.xaml.cs"::::::code language="xaml" source="~/../code-windows/components/HeaderedControls/samples/HeaderedContentControlTextSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/HeaderedControls/samples/HeaderedContentControlTextSample.xaml.cs"::::::code language="xaml" source="~/../code-windows/components/HeaderedControls/samples/HeaderedContentControlImageSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/HeaderedControls/samples/HeaderedContentControlImageSample.xaml.cs"::::::code language="xaml" source="~/../code-windows/components/HeaderedControls/samples/HeaderedContentControlComplexSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/HeaderedControls/samples/HeaderedContentControlComplexSample.xaml.cs":::

## Syntax

```xaml
<Page ...
     xmlns:controls="using:CommunityToolkit.WinUI.Controls"/>

<controls:HeaderedContentControl>
    <!-- Header content or HeaderTemplate content -->
</controls:HeaderedContentControl>
```

