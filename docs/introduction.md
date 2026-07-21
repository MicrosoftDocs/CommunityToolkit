---
title: .NET Community Toolkit Introduction
author: Sergio0694
description: The .NET Community Toolkit is a collection of helpers and APIs that work for all .NET developers and are agnostic of any specific UI platform. The toolkit is maintained and published by Microsoft, and part of the .NET Foundation.
ms.date: 03/29/2022
---

# .NET Community Toolkit introduction

[.NET Community Toolkit](https://aka.ms/toolkit/dotnet) is a collection of helpers and APIs that work for all [.NET developers](/dotnet/) and are agnostic of any specific UI platform. The toolkit is maintained and published by Microsoft, and is part of the [.NET Foundation](https://www.dotnetfoundation.org/).

The .NET Community Toolkit is available as a set of NuGet Packages for new or existing .NET projects.

The toolkit contains .NET Standard libraries (originally developed as part of the [Windows Community Toolkit](/windows/communitytoolkit/)) that can be used both by application developers (regardless on the specific UI framework in use) and library authors. These libraries are also being used internally at Microsoft to power many first-party apps (such as the Microsoft Store) and constantly improved by listening to feedbacks from other teams, external partners, and other developers from the community. Here's a quick breakdown of the various components you'll find:

- [`CommunityToolkit.Mvvm` (aka MVVM Toolkit)](mvvm/index.md): A fast, modular, platform-agnostic MVVM library, which is the official successor of [`MvvmLight`](mvvm/migratingfrommvvmlight.md). It's used extensively in the Microsoft Store and other first-party apps.
- `CommunityToolkit.Mvvm.SourceGenerators`: The source generators to augment the MVVM Toolkit.
- [`CommunityToolkit.Diagnostics`](/windows/communitytoolkit/diagnostics/introduction): A set of helper APIs (specifically, Guard and ThrowHelper) that can be used for cleaner, more efficient, and less error-prone argument validation and error checking.
- [`CommunityToolkit.HighPerformance`](/windows/communitytoolkit/high-performance/introduction): A collection of helpers for working in high-performance scenarios. It includes APIs such as pooled buffer helpers, a fast string pool type, a 2D variant of `Memory<T>` and `Span<T>` ([`Memory2D<T>`](/windows/communitytoolkit/high-performance/memory2d) and [`Span2D<T>`](/windows/communitytoolkit/high-performance/span2d)) that also supports discontiguous regions, helpers for bit-shift operations (such as `BitHelper`, also used in [Paint.NET](https://www.getpaint.net/)), and more.
- `CommunityToolkit.Common`: A set of helper APIs shared with other CommunityToolkit libraries.

You can also preview the capabilities of the [MVVM Toolkit](mvvm/index.md) by running the [sample app](https://aka.ms/mvvmtoolkit/samples).

## Get started

For more detailed information about using the toolkit, follow the [Getting started guide](/windows/communitytoolkit/getting-started).

## Open source

The .NET Community Toolkit is an open-source project hosted on GitHub by the community as part of the [.NET Foundation](https://www.dotnetfoundation.org/):

- [.NET Community Toolkit repo](https://aka.ms/toolkit/dotnet)
- [MVVM Toolkit Samples repo](https://aka.ms/mvvmtoolkit/samples)
