---
title: Introduction to the Diagnostics package
author: Sergio0694
description: An overview of how to get started with the Diagnostics package and to the APIs it contains
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, .net community toolkit, csharp, get started, visual studio, diagnostics, exceptions, contract, net core, net standard
---

# Introduction to the Diagnostics package

The `CommunityToolkit.Diagnostics` package contains APIs to efficiently validate method parameters and to throw exceptions in faulting code paths. It is meant to be used to help simplify all argument checks and to make them more expressive and easier to read, while at the same time improving codegen quality and performance.

This package can be installed through NuGet, and it has the following multi-targets:

- .NET Standard 2.0
- .NET Standard 2.1
- .NET 6

This means the package can be used on any available runtime (including .NET Framework, .NET Core, UWP, Unity, Xamarin, Uno, Blazor, etc.). The API surface is almost identical in all cases, while the internal implementation can be optimized when newer APIs are available. The Diagnostics package as a whole is meant to be self-contained and extremely small in scope and binary size.

## Getting started

To install the package from within Visual Studio:

1. In Solution Explorer, right-click on the project and select **Manage NuGet Packages**. Search for **CommunityToolkit.Diagnostics** and install it.

    ![NuGet Packages](../images/get-started/manage-nuget-packages.png "Manage NuGet Packages Image")

2. Add a using or Imports directive to use the new APIs:

    ```c#
    using CommunityToolkit.Diagnostics;
    ```

    ```vb
    Imports CommunityToolkit.Diagnostics
    ```

## Additional resources

You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Diagnostics.UnitTests).