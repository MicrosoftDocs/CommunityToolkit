---
title: ItemsView extensions - .NET MAUI Community Toolkit
author: brminnick
description: The ItemsView extensions provide a series of extension methods that support configuring ItemsView controls
ms.date: 03/28/2022
---

# ItemsView extensions

The `ItemsView` extensions provide a series of extension methods that support configuring `ItemsView` controls such as `CarouselView` and `CollectionView`.

The extensions offer the following methods:

## EmptyView

The `EmptyView` method sets the `EmptyView` property on an `ItemsView` element.

The following example sets the `EmptyView` to a new `Label` with text `"The Collection is Empty"`:

```csharp
new CollectionView().EmptyView(new Label().Text("The Collection is Empty"));
```

## EmptyViewTemplate

The `EmptyViewTemplate` method sets the `EmptyViewTemplate` property on an `ItemsView` element.

The following example sets the `EmptyViewTemplate` to a new `DataTemplate` containing a `Label` with text `"The Collection is Empty"`:

```csharp
new CollectionView().EmptyViewTemplate(new DataTemplate(() => new Label().Text("The Collection is Empty")));
```

## ItemsSource

The `ItemsSource` method sets the `ItemsSource` property on an `ItemsView` element.

The following example sets the `ItemsSource` to `new string[] { "C#", "Markup", "Extensions" }`

```csharp
new CollectionView().ItemsSource(new string[] { "C#", "Markup", "Extensions" });
```

## HorizontalScrollBarVisibility

The `HorizontalScrollBarVisibility` method sets the `HorizontalScrollBarVisibility` property on an `ItemsView` element.

The following example sets the `HorizontalScrollBarVisibility` to `ScrollBarVisibility.Never`:

```csharp
new CollectionView().HorizontalScrollBarVisibility(ScrollBarVisibility.Never);
```

## VerticalScrollBarVisibility

The `VerticalScrollBarVisibility` method sets the `VerticalScrollBarVisibility` property on an `ItemsView` element.

The following example sets the `VerticalScrollBarVisibility` to `ScrollBarVisibility.Never`

```csharp
new CollectionView().VerticalScrollBarVisibility(ScrollBarVisibility.Never);
```

## ScrollBarVisibility

The `ScrollBarVisibility` method sets both the `VerticalScrollBarVisibility` and `HorizontalScrollBarVisibility` properties on an `ItemsView` element.

The following example sets both the `VerticalScrollBarVisibility` and `HorizontalScrollBarVisibility` to `ScrollBarVisibility.Never`:

```csharp
new CollectionView().ScrollBarVisibility(ScrollBarVisibility.Never);
```

## RemainingItemsThreshold

The `RemainingItemsThreshold` method sets the `RemainingItemsThreshold` property on an `ItemsView` element.

The following example sets the `RemainingItemsThreshold` to `10`:

```csharp
new CollectionView().RemainingItemsThreshold(10);
```

## RemainingItemsThresholdReachedCommand

The `RemainingItemsThresholdReachedCommand` method sets the `RemainingItemsThresholdReachedCommand` property on an `ItemsView` element.

The following example sets the `RemainingItemsThresholdReachedCommand` to a new `Command`:

```csharp
new CollectionView().RemainingItemsThresholdReachedCommand(new Command(async () => await DisplayAlert("Threshold Reached", "", "OK")));
```

Theere is a second overload that sets both the `RemainingItemsThresholdReachedCommand` property and the `RemainingItemsThresholdReachedCommandParameter` property.

The following example sets the `RemainingItemsThresholdReachedCommand` to a new `Command<string>` and sets the `RemainingItemsThresholdReachedCommandParameter` to `"No Items Remaining"`:

```csharp
new CollectionView().RemainingItemsThresholdReachedCommand(new Command<string>(async text => await DisplayAlert("Threshold Reached", text, "OK"), "No Items Remaining"));
```

## RemainingItemsThresholdReachedCommandParameter

The `RemainingItemsThresholdReachedCommandParameter` method sets the `RemainingItemsThresholdReachedCommandParameter` property on an `ItemsView` element.

The following example sets the `RemainingItemsThresholdReachedCommandParameter` to `"Hello World"`:

```csharp
new CollectionView().RemainingItemsThresholdReachedCommandParameter("Hello World");
```

## ItemTemplate

The `ItemTemplate` method sets the `ItemTemplate` property on an `ItemsView` element.

The following example sets the `ItemTemplate` to a new `DataTemplate` containing a `Label` whose `TextProperty` is bound to the ItemsSource:

```csharp
new CollectionView().ItemTemplate(new DataTemplate(() => new Label().Bind(Label.TextProperty, Binding.SelfPath)));
```

## ItemsUpdatingScrollMode

The `ItemsUpdatingScrollMode` method sets the `ItemsUpdatingScrollMode` property on an `ItemsView` element.

The following example sets the `ItemsUpdatingScrollMode` to `ItemsUpdatingScrollMode.KeepLastItemInView`:

```csharp
new CollectionView().ItemsUpdatingScrollMode(ItemsUpdatingScrollMode.KeepLastItemInView);
```
