---
title: .NET Community Toolkit Introduction
author: Sergio0694
description: The .NET Community Toolkit is a collection of helpers and APIs that work for all .NET developers and are agnostic of any specific UI platform. The toolkit is maintained and published by Microsoft, and part of the .NET Foundation.
ms.date: 03/29/2022
---

# .NET Community Toolkit Introduction

[.NET Community Toolkit][repo-url] is a collection of helpers and APIs that work for all [.NET developers](/dotnet/) and are agnostic of any specific UI platform. The toolkit is maintained and published by Microsoft, and part of the [.NET Foundation][dotnet-foundation].

The .NET Community Toolkit is available as a set of NuGet Packages for new or existing .NET projects.

The toolkit contains .NET Standard libraries (originally developed as part of the [Windows Community Toolkit][windows-community-toolkit]) that can be used both by application developers (regardless on the specific UI framework in use) and library authors. These libraries are also being used internally at Microsoft to power many of our first party apps (such as the new Microsoft Store) and constantly improved by listening to feedbacks from other teams, external partners, and other developers from the community. Here's a quick breakdown of the various components you'll find:

- [`CommunityToolkit.Mvvm` (aka MVVM Toolkit)][mvvm-toolkit-intro]: a fast, modular, platform-agnostic MVVM library, which is the official successor of [`MvvmLight`][mvvmlight-migration]. It's used extensively in the Microsoft Store and other first party apps.
- `CommunityToolkit.Mvvm.SourceGenerators`: the source generators to augment the MVVM Toolkit.
- [`CommunityToolkit.Diagnostics`][diagnostics-intro]: a set of helper APIs (specifically, Guard and ThrowHelper) that can be used for cleaner, more efficient and less error-prone argument validation and error checking.
- [`CommunityToolkit.HighPerformance`][hp-intro] a collection of helpers for working in high-performance scenarios. It includes APIs such as pooled buffer helpers, a fast string pool type, a 2D variant of `Memory<T>` and `Span<T>` ([`Memory2D<T>`][hp-memory2d] and [`Span2D<T>`][hp-span2d]) also supporting discontiguous regions, helpers for bit shift operations (such as `BitHelper`, also used in [Paint.NET][paint-net]), and more.
- `CommunityToolkit.Common`: a set of helper APIs shared with other CommunityToolkit libraries.

You can also preview the capabilities of the [MVVM Toolkit][mvvm-toolkit-intro] by running the [sample app available here][mvvm-toolkit-samples].

Feel free to browse the documentation using the table of contents on the left side of this page.

[repo-url]: https://aka.ms/toolkit/dotnet ".NET Community Toolkit GitHub Repository"
[dotnet-foundation]: https://www.dotnetfoundation.org/ ".NET Foundation Home Page"
[windows-community-toolkit]: /windows/communitytoolkit/ "Windows Community Toolkit Documentation"
[mvvm-toolkit-intro]: mvvm/index.md "MVVM Toolkit Introduction"
[mvvm-toolkit-samples]: https://aka.ms/mvvmtoolkit/samples "MVVM Toolkit Samples"
[mvvmlight-migration]: mvvm/migratingfrommvvmlight.md "MVVMLight Migration Documentation"
[diagnostics-intro]: /windows/communitytoolkit/diagnostics/introduction "Diagnostics Package Introduction"
[hp-intro]: /windows/communitytoolkit/high-performance/introduction "High Performance Package Introduction"
[hp-memory2d]: /windows/communitytoolkit/high-performance/memory2d "Memory2D&lt;T&gt; Documentation"
[hp-span2d]: /windows/communitytoolkit/high-performance/span2d "Span2D&lt;T&gt; Documentation"
[paint-net]: https://www.getpaint.net/ "Paint.NET Home Page"

## [Get started][get-started]

Follow the [Getting started guide][get-started] for more detailed information about using the toolkit.

[get-started]: /windows/communitytoolkit/getting-started "Getting started guide"

## Open source

The .NET Community Toolkit is an open source project hosted on GitHub by the community as part of the [.NET Foundation][dotnet-foundation]:

- [.NET Community Toolkit repo][repo-url]

- [MVVM Toolkit Samples repo][mvvm-toolkit-samples]
