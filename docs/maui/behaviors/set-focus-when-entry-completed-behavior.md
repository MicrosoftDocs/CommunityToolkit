---
title: SetFocusOnEntryCompletedBehavior - .NET MAUI Community Toolkit
author: bijington
description: "The SetFocusOnEntryCompletedBehavior is a Behavior that allows the user to validate a given text depending on specified parameters."
ms.date: 05/18/2022
---

# SetFocusOnEntryCompletedBehavior

The `SetFocusOnEntryCompletedBehavior` is a `Behavior` that gives focus to a specified `VisualElement` when an `Entry` is completed. For example, a page might have several `Entry`s in sequence, and this makes it convenient to the user if completing an `Entry` automatically switched focus to the next `Entry`.

## Syntax

The following examples show how to add the `SetFocusOnEntryCompletedBehavior` to an `Entry` so that when the `Next` button on the soft keyboard is pressed another `Entry` is given focus.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the SetFocusOnEntryCompletedBehavior

The `SetFocusOnEntryCompletedBehavior` can be used as follows in XAML:

```xaml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage
    x:Class="CommunityToolkit.Maui.Sample.Pages.Behaviors.SetFocusOnEntryCompletedBehaviorPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit">

    <VerticalStackLayout Spacing="12">

        <Entry
            x:Name="FirstNameEntry"
            toolkit:SetFocusOnEntryCompletedBehavior.NextElement="{x:Reference LastNameEntry}"
            Placeholder="Entry 1 (Tap `Next` on the keyboard when finished)"
            ReturnType="Next" />
    
        <Entry
            x:Name="LastNameEntry" />

    </VerticalStackLayout>
</ContentPage>
```

### C#

The `SetFocusOnEntryCompletedBehavior` can be used as follows in C#:

```csharp
class SetFocusOnEntryCompletedBehaviorPage : ContentPage
{
    public SetFocusOnEntryCompletedBehaviorPage()
    {
        var firstName = new Entry
        {
            Placeholder = "Entry 1 (Tap `Next` on the keyboard when finished)",
            ReturnType = ReturnType.Next
        };

        var lastName = new Entry();

        SetFocusOnEntryCompletedBehavior.SetNextElement(firstName, lastName);

        Content = new VerticalStackLayout
        {
            Spacing = 12,
            Children = 
            {
                firstName,
                lastName
            }
        };
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this behavior in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class SetFocusOnEntryCompletedBehaviorPage : ContentPage
{
    public SetFocusOnEntryCompletedBehaviorPage()
    {
        Content = new VerticalStackLayout
        {
            Spacing = 12,
            Children = 
            {
                new Entry { ReturnType = ReturnType.Next }
                    .Assign(out var firstName)
                    .Placeholder("Entry 1 (Tap `Next` on the keyboard when finished)"),

                new Entry()
                    .Assign(out var lastName)
            }
        };

        SetFocusOnEntryCompletedBehavior.SetNextElement(firstName, lastName);
    }
}
```

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/SetFocusOnEntryCompletedBehaviorPage.xaml).

## API

You can find the source code for `SetFocusOnEntryCompletedBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/SetFocusOnEntryCompletedBehavior.cs).
