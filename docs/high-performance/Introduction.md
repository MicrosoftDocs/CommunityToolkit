---
title: Introduction to the High Performance package
author: Sergio0694
description: An overview of how to get started with the High Performance package and to the APIs it contains
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, get started, visual studio, high performance, net core, net standard
---

# Introduction to the High Performance package

The `CommunityToolkit.HighPerformance` contains helpers and extensions to work in high-performance scenarios. This package can be installed through NuGet, and it has the following multi-targets:

- .NET Standard 2.0
- .NET Standard 2.1
- .NET 6
- .NET 7

This means that you can use it from anything from UWP or legacy .NET Framework applications, games written in Unity, cross-platform mobile applications using Xamarin, to .NET Standard libraries and modern .NET 6 and .NET 7 applications. The API surface is almost identical in all cases, and lots of work has been put into backporting as many features as possible to older targets like .NET Standard 2.0. Except for some minor differences, you can expect the same APIs to be available on all target frameworks. The reason why multi-targeting has been used is to allow the package to leverage all the latest APIs on modern runtimes (like .NET 7) whenever possible, while still offering most of its functionalities to all target platforms.

## Getting started

To install the package from within Visual Studio:

1. In Solution Explorer, right-click on the project and select **Manage NuGet Packages**. Search for **CommunityToolkit.HighPerformance** and install it.

    ![NuGet Packages](../images/get-started/manage-nuget-packages.png "Manage NuGet Packages Image")

2. Add a using or Imports directive to use the new APIs:

    ```c#
    using CommunityToolkit.HighPerformance;
    ```

    ```vb
    Imports CommunityToolkit.HighPerformance
    ```

3. Code samples are available in the other docs pages for the MVVM Toolkit, and in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.HighPerformance.UnitTests) for the project.

## When should I use this package?

As the name suggests, the High Performance package contains a set of APIs that are heavily focused on optimization. All the new APIs have been carefully crafted to achieve the best possible performance when using them, either through reduced memory allocation, micro-optimizations at the assembly level, or by structuring the APIs in a way that facilitates writing performance oriented code in general.

This package makes heavy use of APIs such as:

- [`System.Span<T>`](/dotnet/api/system.span-1)
- [`System.Memory<T>`](/dotnet/api/system.memory-1)
- [`System.Buffers.ArrayPool<T>`](/dotnet/api/system.buffers.arraypool-1)
- [`System.Runtime.CompilerServices.Unsafe`](/dotnet/api/system.runtime.compilerservices.unsafe)
- [`System.Runtime.InteropServices.MemoryMarshal`](/dotnet/api/system.runtime.interopservices.memorymarshal)
- [`System.Threading.Tasks.Parallel`](/dotnet/api/system.threading.tasks.parallel)

If you are already familiar with these APIs or even if you're just getting started with writing high performance code in C# and want a set of well tested helpers to use in your own projects, have a look at what's included in this package to see how you can use it in your own projects!

## Where to start?

Here are some APIs you could look at first, if you were already using one of those types mentioned above:

- [`Span2D<T>`](Span2D.md) and [`Memory2D<T>`](Memory2D.md), for a `Span<T>` and `Memory<T>`-like abstraction over 2D memory
- [`MemoryOwner<T>`](MemoryOwner.md) and [`SpanOwner<T>`](SpanOwner.md), if you were using `System.Buffers.ArrayPool<T>`.
- [`StringPool`](StringPool.md), for an `ArrayPool<T>`-like type to cache `string` instances
- [`ParallelHelper`](ParallelHelper.md), if you were using `System.Threading.Tasks.Parallel`.

## Additional resources

You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.HighPerformance.UnitTests).