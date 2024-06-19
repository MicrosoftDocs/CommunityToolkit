---
title: Getting Started with NativeLibraryInterop
author: miparker, rachelkang
description: The NativeLibraryInterop build tasks are available via a NuGet package that can be added to any existing or new .NET MAUI project.
ms.date: 06/18/2024
---

# Getting Started with NativeLibraryInterop

This article covers how to get started with creating a slim binding using Maui.NativeLibraryInterop to simplify the setup. This does not provide a detailed step-by-step walkthrough but rather outlines the basic steps and some key decision points.

## Set up native binding library

// mention newBinding template and the simple edits that can be made there
// using the NuGet - referencing in csproj

### Android

`dotnet new android-bindinglib`
// link to docs

### iOS & MacCatalyst

`dotnet new iosbinding`
// link to docs

## Create API interface

// mention newBinding template and the simple edits that can be made there

### Android

// instructions for Android Studio project creation
// Java file - APIs here

### iOS & MacCatalyst

// instructions for Xcode project creation
// Swift file - APIs here
// copying ApiDefinitions over

## Consume the APIs in your .NET MAUI app

// mention newBinding template and the simple edits that can be made there
// csproj references