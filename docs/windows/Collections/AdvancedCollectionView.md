---
title: AdvancedCollectionView
author: nmetulev
description: The AdvancedCollectionView is a collection view implementation that support filtering, sorting and incremental loading. It's meant to be used in a viewmodel.
keywords: AdvancedCollectionView, data, sorting, filtering, Collections
dev_langs:
  - csharp
category: Helpers
subcategory: Data
discussion-id: 0
issue-id: 0
icon: Assets/AdvancedCollectionView.png
---

# AdvancedCollectionView

:::code language="xaml" source="~/../code-windows/components/Collections/samples/AdvancedCollectionViewSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Collections/samples/AdvancedCollectionViewSample.xaml.cs":::

## Usage

In your viewmodel instead of having a public [IEnumerable](/dotnet/core/api/system.collections.generic.ienumerable-1) of some sort to be bound to an eg. [Listview](/uwp/api/Windows.UI.Xaml.Controls.ListView), create a public AdvancedCollectionView and pass your list in the constructor to it. If you've done that you can use the many useful features it provides:

* sorting your list using the `SortDirection` helper: specify any number of property names to sort on with the direction desired
* filtering your list using a [Predicate](/dotnet/core/api/system.predicate-1): this will automatically filter your list only to the items that pass the check by the predicate provided
* deferring notifications using the `NotificationDeferrer` helper: with a convenient _using_ pattern you can increase performance while doing large-scale modifications in your list by waiting with updates until you've completed your work
* incremental loading: if your source collection supports the feature then AdvancedCollectionView will do as well (it simply forwards the calls)
* live shaping: when constructing the `AdvancedCollectionView` you may specify that the collection use live shaping. This means that the collection will re-filter or re-sort if there are changes to the sort properties or filter properties that are specified using `ObserveFilterProperty`

## Example

```csharp
using CommunityToolkit.WinUI.Collections;

// Grab a sample type
public class Person
{
    public string Name { get; set; }
}

// Set up the original list with a few sample items
var oc = new ObservableCollection<Person>
{
    new Person { Name = "Staff" },
    new Person { Name = "42" },
    new Person { Name = "Swan" },
    new Person { Name = "Orchid" },
    new Person { Name = "15" },
    new Person { Name = "Flame" },
    new Person { Name = "16" },
    new Person { Name = "Arrow" },
    new Person { Name = "Tempest" },
    new Person { Name = "23" },
    new Person { Name = "Pearl" },
    new Person { Name = "Hydra" },
    new Person { Name = "Lamp Post" },
    new Person { Name = "4" },
    new Person { Name = "Looking Glass" },
    new Person { Name = "8" },
};

// Set up the AdvancedCollectionView with live shaping enabled to filter and sort the original list
var acv = new AdvancedCollectionView(oc, true);

// Let's filter out the integers
int nul;
acv.Filter = x => !int.TryParse(((Person)x).Name, out nul);

// And sort ascending by the property "Name"
acv.SortDescriptions.Add(new SortDescription("Name", SortDirection.Ascending));

// Let's add a Person to the observable collection
var person = new Person { Name = "Aardvark" };
oc.Add(person);

// Our added person is now at the top of the list, but if we rename this person, we can trigger a re-sort
person.Name = "Zaphod"; // Now a re-sort is triggered and person will be last in the list

// AdvancedCollectionView can be bound to anything that uses collections. 
YourListView.ItemsSource = acv;
```

## Remarks

_What source can I use?_

It's not necessary to use an eg. [ObservableCollection](/dotnet/core/api/system.collections.objectmodel.observablecollection-1) to use the AdvancedCollectionView. It works as expected even when providing a simple [List](/dotnet/core/api/system.collections.generic.list-1) in the constructor.

_Any performance guidelines?_

If you're removing, modifying or inserting large amounts of items while having filtering and/or sorting set up, it's recommended that you use the `NotificationDeferrer` helper provided. It skips any performance heavy logic while it's in use, and automatically calls the `Refresh` method when disposed.

```csharp
using (acv.DeferRefresh())
{
    for (var i = 0; i < 500; i++)
    {
        acv.Add(new Person { Name = "defer" });
    }
} // acv.Refresh() gets called here
```

