---
title: SelectAllTextBehavior - .NET MAUI Community Toolkit
author: vhugogarcia
description: "The SelectAllTextBehavior is an effect that will select all text in an Entry / Editor when it becomes focused."
ms.date: 09/12/2023
---

# SelectAllTextBehavior

The `SelectAllTextBehavior` is an `Behavior` that will select all text in an `Entry` / `Editor` when it becomes focused.

## Syntax

The following examples show how to add the `SelectAllTextBehavior` to an `Entry`.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the SelectAllTextBehavior

The `SelectAllTextBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Behaviors.SelectAllTextBehaviorPage">

    <Entry>
        <Entry.Behaviors>
            <toolkit:SelectAllTextBehavior />
        </Entry.Behaviors>
    </Entry>

</ContentPage>
```

### C#

The `SelectAllTextBehavior` can be used as follows in C#:

```csharp
class SelectAllTextBehaviorPage : ContentPage
{
    public SelectAllTextBehaviorPage()
    {
        var entry = new Entry();

        var selectAllTextBehavior = new SelectAllTextBehavior();

        entry.Behaviors.Add(selectAllTextBehavior);

        Content = entry;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class SelectAllTextBehaviorPage : ContentPage
{
    public SelectAllTextBehaviorPage()
    {
        Content = new Entry()
            .Behaviors(new SelectAllTextBehavior());
    }
}
```

> [!NOTE]
> On MacCatalyst, the behavior “SelectAllText” only works by doing right-click on the `editor` due to a native platform behavior.

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/SelectAllTextBehaviorPage.xaml).