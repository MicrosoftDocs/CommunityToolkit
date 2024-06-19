---
title: Native Library Interop - .NET MAUI Community Toolkit
author: miparker, rachelkang
description: The .NET MAUI Community Toolkit Native Library Interop components
ms.date: 06/18/2024
---

# Native Library Interop

## Overview

Native Library Interop, formerly referred to as "Slim Bindings", refers to a pattern for accessing native SDKs in .NET apps. The idea is to create your own abstraction or thin "wrapper" with a simplified API surface to the native SDKs you're interested in calling from .NET. The native "wrapper" library/framework projects get created in Android Studio using Java/Kotlin and/or Xcode using Objective-C/Swift. This approach is especially beneficial when you only need a small slice of the API surface of the SDK, though it also works well for larger API surface usage all the same.

### Understanding when and why to use Native Library Interop

Native Library Interop is a very effective approach to interop with native libraries, but they may not always be the best fit for your project. Generally, if you are already maintaining bindings and are comfortable continuing to do so, there's no need to change approaches. It may also be worth considering a traditional/full binding if the library you are needing to interop with has a large API surface and you need to use the majority of those APIs, or if you are a vendor of a library/SDK and you are wanting to support .NET MAUI developers in consuming your library. The existing tools and methods for traditional bindings aren't going away; this is simply an alternative technique which is in some cases much easier to understand, implement, and maintain.

A key benefit of Native Library Interop is based on the premise that .NET Android and iOS binding tools work great with simple API surfaces. Assuming the wrapper contains only primitive types which .NET already knows about and has bindings for, the existing binding tools are able to more reliably generate working binding definitions without the amount of manual intervention often required for traditional bindings.

While the initial setup may take some time, handling subsequent updates to the underlying SDKs may involve less work. For example, it may only require updating the version and rebuilding. If there's breaking changes to the API surfaces being used, or to how SDKs work in general, then native code may need changing. However, there's a greater chance that the wrapper API surface (and the usage in the .NET app) can remain unchanged compared to traditional full bindings.

The implementation of the wrapper API would typically follow the SDK documentation which is likely easier to follow and apply when using the same language as the documentation. It may even be possible to copy and paste code from the vendor documentation directly.

### Using Maui.NativeLibraryInterop

A notable challenge with creating and maintaining bindings created via Native Library Interop is manually coalescing the native projects, their native dependencies, build outputs, and the .NET Binding library project. Maui.NativeLibraryInterop can help orchestrate parts of this process through MSBuild invocations. This can include:

- Resolving or downloading native SDK dependencies
- Building the native slim binding project and its dependencies
- Moving the requisite native artifacts to the expected working directory
- Generating the API definition for the binding library project

The [NativeLibraryInterop.BuildTasks NuGet package](#nuget-package) provides a set of build tasks and targets you can configure in a .NET binding library project csproj file. See [examples](#examples).

Android binding projects generate the API definition automatically taking into account any optional manual modifications like those implemented via the [Metadata.xml](https://learn.microsoft.com/xamarin/android/platform/binding-java-library/customizing-bindings/java-bindings-metadata#metadataxml-transform-file) transform file.

![Conceptual overview: NativeLibraryInterop for Android](../images/native-library-interop/nativelibraryinterop-conceptual-overview-android.png "Conceptual overview of NativeLibraryInterop for Android")

An iOS binding library project must include an explicitly defined API. To help with this, [Objective-Sharpie](https://learn.microsoft.com/xamarin/cross-platform/macios/binding/objective-sharpie/#overview) can be run automatically on the resulting native framework to produce an [API definition file](https://learn.microsoft.com/xamarin/cross-platform/macios/binding/objective-c-libraries?tabs=macos#The_API_definition_file) (ApiDefinition.cs) alongside it. This can serve as a helpful reference when creating and maintaining the ApiDefintion.cs file used by the iOS binding project.

![Conceptual overview: NativeLibraryInterop for iOS](../images/native-library-interop/nativelibraryinterop-conceptual-overview-ios.png "Conceptual overview of NativeLibraryInterop for iOS")

## Examples

### Building the native wrapper - Android

```xml
<ItemGroup>
    <GradleProjectReference Include="../native" >
        <ModuleName>{module_name}</ModuleName>
        <!-- Metadata applicable to @(AndroidLibrary) will be used if set -->
        <Bind>true</Bind>
        <Pack>true</Pack>
    </GradleProjectReference>
</ItemGroup>
```

### Building the native wrapper - iOS

```xml
<ItemGroup>
    <XcodeProjectReference Include="../native/{project_name}.xcodeproj">
        <SchemeName>{scheme_name}</SchemeName>
        <SharpieNamespace>{namespace_to_generate}</SharpieNamespace>
        <SharpieBind>true</SharpieBind>
        <!-- Metadata applicable to @(NativeReference) will be used if set -->
        <Kind>Framework</Kind>
        <SmartLink>true</SmartLink>
    </XcodeProjectReference>
</ItemGroup>
```

## NuGet package

The NativeLibraryInterop.BuildTasks package can be included in your project(s) as described in our [Getting started](get-started.md) guide.

## Resources

- [GoneMobile.io: Slim Bindings Podcast Episode](https://www.gonemobile.io/101)
- [MonkeyFest 2020: Bridge the gap with Bindings to native iOS and Android SDK's](https://www.youtube.com/watch?v=bgK_6anwMcw)
