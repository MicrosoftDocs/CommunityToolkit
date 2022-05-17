---
title: DynamicResourceHandler extensions - .NET MAUI Community Toolkit
author: brminnick
description: The Dynamic Resource Handler extensions provide a series of extension methods that support configuring IDynamicResourceHandler
ms.date: 05/16/2022
---

# DynamicResourceHandler extensions

[!INCLUDE [docs under construction](../../includes/preview-note.md)]

The `DynamicResourceHandler` extensions provide a series of extension methods that support configuring `IDynamicResourceHandler` which can be used to [Theme an App](/dotnet/maui/user-interface/theming).

The extensions offer the following methods:

## DynamicResource

The `DynamicResource` method sets the `DynamicResource` property on a control implementing `IDynamicResourceHandler`.

The following example binds `Label.TextColorProperty` to the `DynamicResource`, [ResourceDictionary](/dotnet/maui/fundamentals/resource-dictionaries) key `TextColor`:

```csharp
new Label().DynamicResource(Label.TextColorProperty, "TextColor");
```

## DynamicResources

The `DynamicResources` method sets multiple `DynamicResource` properties on a control implementing `IDynamicResourceHandler`.

The following example binds `Label.TextColorProperty` to the [ResourceDictionary](/dotnet/maui/fundamentals/resource-dictionaries) key `TextColor`, and binds `Label.FontFamilyProperty` to the [ResourceDictionary](/dotnet/maui/fundamentals/resource-dictionaries) key `FontFamily`,

```csharp
new Label().DynamicResources(Label.TextColorProperty, "TextColor", 
                                Label.FontFamilyProperty, "FontFamily", );
```
