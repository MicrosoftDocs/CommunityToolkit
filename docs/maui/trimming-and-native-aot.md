---
title: Trimming and Native AOT - .NET MAUI Community Toolkit
author: TheCodeTraveler
description: "The .NET MAUI Community Toolkit packages are trim-safe and Native AOT-safe. Learn which platforms are supported, how to see trim warnings, the two features that need your attention, and a .NET MAUI issue with CollectionView item templates in fully trimmed Windows apps."
ms.date: 11/13/2026
---

# Trimming and Native AOT

The `CommunityToolkit.Maui`, `CommunityToolkit.Maui.Core`, `CommunityToolkit.Maui.Camera` and `CommunityToolkit.Maui.MediaElement` packages are trim-safe and Native AOT-safe. The packages produce no trim or AOT warnings, and no feature is removed when you trim.

Two features need your attention:

- [Validation behaviors](#validate-a-property-that-is-not-a-bindableproperty): `ValuePropertyName` must name a `BindableProperty`.
- [Windows offline speech-to-text](#windows-offline-speech-to-text): it needs one project setting and isn't available with Native AOT.

A fully trimmed Windows app may also need a workaround for a .NET MAUI issue: see [Windows CollectionView item templates](#windows-collectionview-item-templates).

## Supported platforms

| Platform | Full trimming | Native AOT |
|---|---|---|
| iOS | Supported | Supported |
| Mac Catalyst | Supported | Supported |
| Android | Supported | Experimental in .NET 11 |
| Windows | Supported | Not supported |

Native AOT isn't supported on Windows. A .NET MAUI app published with `PublishAot` on Windows builds, but crashes at run time, because of a bug in .NET MAUI: [dotnet/maui#39053](https://github.com/dotnet/maui/issues/39053).

> [!NOTE]
> If [dotnet/maui#39053](https://github.com/dotnet/maui/issues/39053) is fixed and this page still says unsupported, please [open an issue in CommunityToolkit/Maui](https://github.com/CommunityToolkit/Maui/issues/new/choose) so we can enable and test it.

## Default trimming per platform

| Platform | Default in Release builds |
|---|---|
| Android | Partial trimming |
| Mac Catalyst | Partial trimming |
| iOS device | Partial trimming |
| iOS simulator | Not trimmed |
| Windows | Not trimmed, unless you opt in with `<PublishTrimmed>true</PublishTrimmed>` in a self-contained publish |
| Any platform with Native AOT | Always full trimming |

Partial trimming trims the toolkit as hard as full trimming does, because the toolkit packages are trimmable. The toolkit behaves the same with `TrimMode` set to `full`. Your own code and other libraries can still break; the warnings show where.

## See trim and AOT warnings

.NET MAUI hides trim warnings in apps that use the default partial trimming. To see them, set full trimming or publish with Native AOT:

```xml
<PropertyGroup>
    <TrimMode>full</TrimMode>
</PropertyGroup>
```

```xml
<PropertyGroup>
    <PublishAot>true</PublishAot>
</PropertyGroup>
```

Warnings that point into `CommunityToolkit.Maui.*` assemblies are bugs in the toolkit. Please [open an issue](https://github.com/CommunityToolkit/Maui/issues/new/choose).

## Validate a property that is not a BindableProperty

The validation behaviors (for example `TextValidationBehavior`, `EmailValidationBehavior`, `NumericValidationBehavior`) read the value to validate from a `BindableProperty` named by `ValuePropertyName`. The name must belong to a `BindableProperty`, including inherited ones and your own, declared in a `public static` field named `<Name>Property`, such as `TextProperty` for `Text`. An `internal` field, or one with a different name, makes the behavior throw.

For any other property, such as a plain CLR property or a dotted path, set `ValuePropertyName` to `{x:Null}` first, then bind `Value` with a compiled binding. With `ValuePropertyName` set to `null` or empty, the behavior binds nothing and keeps your `Value` binding.

### [XAML](#tab/xaml)

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             xmlns:local="clr-namespace:MyApp"
             x:Class="MyApp.MainPage">

    <local:MyView x:Name="myView">
        <local:MyView.Behaviors>
            <toolkit:TextValidationBehavior
                ValuePropertyName="{x:Null}"
                Value="{Binding MyProperty, Source={x:Reference myView}, x:DataType=local:MyView}"
                MinimumLength="3" />
        </local:MyView.Behaviors>
    </local:MyView>
</ContentPage>
```

### [C#](#tab/csharp)

```csharp
var behavior = new TextValidationBehavior
{
    ValuePropertyName = null,
    MinimumLength = 3
};

behavior.SetBinding(
    ValidationBehavior.ValueProperty,
    Binding.Create(static (MyView view) => view.MyProperty, source: myView));

myView.Behaviors.Add(behavior);
```

---

When `ValuePropertyName` names something that isn't a `BindableProperty`, such as a plain CLR property, a dotted path or a typo:

- The behavior throws an `ArgumentException` when it attaches, or when you change `ValuePropertyName` while it's attached. The message names the property, says no `public static` `BindableProperty` field `<Name>Property` exists on the view, and shows this fix.
- When exceptions in behaviors are suppressed (you call `options.SetShouldSuppressExceptionsInBehaviors(true)`, see [Options](options.md#setshouldsuppressexceptionsinbehaviors)), the behavior writes a `Trace` message instead and leaves `Value` unbound.

> [!IMPORTANT]
> Earlier versions accepted plain CLR property names and dotted paths. They no longer work and now throw on attach. Replace them with the compiled `Value` binding above.
>
> Set `ValuePropertyName` to `{x:Null}` before you bind `Value`. If you bind `Value` while the attached behavior follows a `BindableProperty`, changing the name to `null` later removes your binding.
>
> `ValuePropertyName="{x:Null}"` used to bind `Value` to the view itself and replace your `Value` binding. It now binds nothing and keeps your binding.

## Windows offline speech-to-text

On Windows, `OfflineSpeechToText` uses `System.Speech`, which needs built-in COM interop. Trimmed apps turn that off by default.

In a trimmed Windows app, with partial or full trimming, add this to the project file:

```xml
<PropertyGroup>
    <BuiltInComInteropSupport>true</BuiltInComInteropSupport>
</PropertyGroup>
```

Without it, `OfflineSpeechToText` throws a `NotSupportedException` naming this setting when you start listening.

No other setting is needed with `TrimMode` set to `full`: the toolkit keeps the COM interfaces of `System.Speech`. It keeps them only when your app uses `OfflineSpeechToText`. If your app calls `System.Speech` directly in a fully trimmed build, for example `SpeechRecognitionEngine` or `SpeechSynthesizer`, it must keep those COM interfaces itself.

`OfflineSpeechToText` isn't available with Native AOT, which doesn't support built-in COM. Windows Native AOT isn't supported for another reason too (see [Supported platforms](#supported-platforms)). The online `SpeechToText` isn't affected.

## Windows CollectionView item templates

This .NET MAUI issue affects your app, not the toolkit. In a Windows app trimmed with `TrimMode` set to `full`, a `CollectionView` shows no templated items when it uses the legacy Windows handler (`<UseWindowsCollectionView2Handler>false</UseWindowsCollectionView2Handler>`). WinUI reads the properties of the .NET MAUI type `ItemTemplateContext`, and of `GroupTemplateContext` for grouped items, through reflection, and the trimmer removes them. See [dotnet/maui#31227](https://github.com/dotnet/maui/issues/31227).

To keep those properties, add these attributes to `CreateMauiApp` in `MauiProgram.cs`. They apply to Windows only:

```csharp
#if WINDOWS
    [System.Diagnostics.CodeAnalysis.DynamicDependency(System.Diagnostics.CodeAnalysis.DynamicallyAccessedMemberTypes.PublicProperties, typeof(Microsoft.Maui.Controls.Platform.ItemTemplateContext))]
    [System.Diagnostics.CodeAnalysis.DynamicDependency(System.Diagnostics.CodeAnalysis.DynamicallyAccessedMemberTypes.PublicProperties, "Microsoft.Maui.Controls.Platform.GroupTemplateContext", "Microsoft.Maui.Controls")]
#endif
    public static MauiApp CreateMauiApp()
```

## See also

- [Trim self-contained deployments and executables](/dotnet/core/deploying/trimming/trim-self-contained)
- [Native AOT deployment](/dotnet/core/deploying/native-aot/)
- [Trim a .NET MAUI app](/dotnet/maui/deployment/trimming)
- [Native AOT deployment on iOS and Mac Catalyst](/dotnet/maui/deployment/nativeaot)
- [Prepare .NET libraries for trimming](/dotnet/core/deploying/trimming/prepare-libraries-for-trimming)
