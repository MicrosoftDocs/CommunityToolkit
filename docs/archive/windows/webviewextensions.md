---
title: WebViewExtensions
author: nmetulev
description: The WebViewExtensions class allows attaching HTML content to a WebView control through XAML directly or through a binding
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, WebViewExtensions, webview, extensions
---

# WebViewExtensions (Archived)

> [!WARNING]
> This component has been archived and is not available in the current version of the Windows Community Toolkit.
>
> While there are no immediate plans to port this component to 8.x, community interest could potentially lead to its inclusion. The component would require significant changes related to WebView2 integration.
>
> For more information:
> - [Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Windows)
> - [Documentation feedback and suggestions](https://github.com/MicrosoftDocs/CommunityToolkit/issues)
>
> Original documentation follows below.

---

The [`WebViewExtensions`](/dotnet/api/microsoft.toolkit.uwp.ui.webviewextensions) allows attaching HTML content to [`WebView`](/uwp/api/windows.ui.xaml.controls.webview).

> **Platform APIs:** [`WebViewExtensions`](/dotnet/api/microsoft.toolkit.uwp.ui.webviewextensions)

## Syntax

Here is how the `WebViewExtensions` properties can be used in XAML:

```xaml
<!-- Attach HTML content directly to a WebView -->
<WebView
    xmlns:ui="using:Microsoft.Toolkit.Uwp.UI"   
    ui:WebViewExtensions.Content="{Binding HtmlContent}" />

<!-- Attach a Uri directly to a WebView -->
<WebView
    xmlns:ui="using:Microsoft.Toolkit.Uwp.UI"
    ui:WebViewExtensions.ContentUri="{Binding ContentUri}" />
```

> [!NOTE]
> In this example, the classic binding syntax is used, but the faster `{x:Bind}` syntax is supported as well. You're free to pick which one to use depending on your use case scenario.

## Examples

You can find more examples in the [unit tests](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/UnitTests).
