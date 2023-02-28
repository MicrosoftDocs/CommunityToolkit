---
title: BindableLayout extensions - .NET MAUI Community Toolkit
author: brminnick
description: The BindableLayout extensions provide a series of extension methods that support configuring its EmptyView, ItemSource and ItemTemplate.
ms.date: 03/28/2022
---

# BindableLayout extensions

The `BindableLayout` extensions provide a series of extension methods that support configuring its `EmptyView`, `ItemSource` and `ItemTemplate`.

## EmptyView

The `EmptyView` method sets the `EmptyView` property on an `ILayout`.

The following example sets the `EmptyView` to `new Label().Text("No Items Found")`:

```csharp
new VerticalStackLayout().EmptyView(new Label().Text("No Items Found"));
```

## EmptyViewTemplate

The `EmptyViewTemplate` method sets the `EmptyViewTemplate` property on an `ILayout`.

The following example sets the `EmptyViewTemplate` to `new DataTemplate(() => new Label().Text("No Items Found"))`:

```csharp
new VerticalStackLayout().EmptyViewTemplate(new DataTemplate(() => new Label().Text("No Items Found")));
```

An overload method exists for `EmptyViewTemplate` that accepts a `Func<object>` that is used to initialize the `DataTemplate`.

```csharp
new VerticalStackLayout().EmptyViewTemplate(() => new Label().Text("No Items Found"));
```

## ItemsSource

The `ItemsSource` method sets the `ItemsSource` property on an `ILayout`.

The following example sets the `EmptyView` to `new Label().Bind(Label.TextProperty, "."))`:

```csharp
new VerticalStackLayout().ItemsSource(new Label().Bind(Label.TextProperty, Binding.SelfPath));
```

## ItemTemplate

The `ItemTemplate` method sets the `ItemTemplate` property on an `ILayout`.

The following example sets the `EmptyViewTemplate` to `new DataTemplate(() => new Label().Bind(Label.TextProperty, ".")`:

```csharp
new VerticalStackLayout().ItemTemplate(new DataTemplate(() => new Label().Bind(Label.TextProperty, Binding.SelfPath)));
```

An overload method exists for `ItemTemplate` that accepts a `Func<object>` that is used to initialize the `DataTemplate`.

```csharp
new VerticalStackLayout().ItemTemplate(() => new Label().Bind(Label.TextProperty, Binding.SelfPath));
```

## ItemTemplateSelector

The `ItemTemplateSelector` method sets the `ItemTemplateSelector` property on an `ILayout`.

The following example sets the `ItemTemplateSelector` to `new CustomDataTemplateSelector()`:

```csharp
new VerticalStackLayout().ItemTemplateSelector(new CustomDataTemplateSelector())

class CustomDataTemplateSelector : DataTemplateSelector
{
  // ...
}
```
