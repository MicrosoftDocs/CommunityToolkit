---
title: WebView extension
author: nmetulev
ms.date: 08/20/2017
description: The UWP Community Toolkit WebView extensions allow attaching HTML content to WebView through XAML directly or through Binding
keywords: windows 10, uwp, uwp community toolkit, uwp toolkit, WebViewExtensions, webview, extensions
---

# WebView extension (Archived)

**Important Note:** This document has been archived and the component is not available in the current version of the Windows Community Toolkit.

While there are no immediate plans to port this component to 8.x, the community is welcome to express interest or contribute to its inclusion.

For more information:
- [Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Windows)
- [Documentation feedback and suggestions](https://github.com/MicrosoftDocs/CommunityToolkit/issues)

Original documentation follows below.

---

> [!WARNING]
> These extensions have been moved to a different type, please refer to docs page for the [`WebViewExtensions`](webviewextensions.md) type.
The **WebViewExtensions** allows attaching HTML content to a WebView.

## Example

```xaml
<!-- Attach HTML content directly to WebView. -->
<WebView extensions:WebView.Content="{Binding HtmlContent}" />

<!-- Attach Uri directly to WebView -->
<WebView extensions:WebView.ContentUri="{Binding ContentUri}" />
```

## Requirements (Windows 10 Device Family)

| [Device family](/windows/uwp/get-started/universal-application-platform-guide) | Universal, 10.0.14393.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Extensions |

## API

* [WebViewExtensions source code](https://github.com/CommunityToolkit/WindowsCommunityToolkit/blob/rel/7.1.0/Microsoft.Toolkit.Uwp.UI/Extensions/WebViewExtensions.cs)
