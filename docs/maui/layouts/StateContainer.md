---
title: StateContainer - .NET MAUI Community Toolkit
author: nicjay
description: StateContainer bindable properties enable any Layout derived element to become state-aware
ms.date: 10/24/2022
---

# StateContainer

Displaying a specific view when your app is in a specific state is a common pattern throughout any mobile app. Examples range from creating loading views to overlay on the screen, or on a subsection of the screen. Empty state views can be created for when there's no data to display, and error state views can be displayed when an error occurs.

## Getting Started

The `StateContainer` attached properties enables the user to turn any layout element like a `VerticalStackLayout`, `HorizontalStackLayout`, or `Grid` into a state-aware layout. Each state-aware layout contains a collection of View derived elements. These elements can be used as templates for different states defined by the user. Whenever the `CurrentState` string property is set to a value that matches the `StateKey` property of one of the View elements, its contents will be displayed instead of the main content. When `CurrentState` is set to null or empty string, the main content is displayed.

> [!NOTE]
> When using `StateContainer` with a `Grid`, any defined states inside it will automatically span every row and column of the `Grid`.

## Syntax

`StateContainer` properties can be used in XAML or C#.

### XAML

```xml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MyProject.MyStatePage">

    <VerticalStackLayout toolkit:StateContainer.CurrentState="{Binding MyCurrentState}">

        <toolkit:StateContainer.StateViews>
            <VerticalStackLayout toolkit:StateView.StateKey="Loading">
                <ActivityIndicator IsRunning="True" />
                <Label Text="Loading Content..." />
            </VerticalStackLayout>
            <Label toolkit:StateView.StateKey="Success" Text="Success!" />
        </toolkit:StateContainer.StateViews>

        <Label Text="Default Content" />

    </VerticalStackLayout>

</ContentPage>
```

### C#

```csharp
using CommunityToolkit.Maui.Layouts;

var stateViews = new List<View>()
{
    new VerticalStackLayout()
    {
        Children =
        {
            new ActivityIndicator() { IsRunning = true },
            new Label() { Text = "Loading Content" }
        }
    },
    new Label() { Text = "Success!" }
};

StateView.SetStateKey(stateViews[0], "Loading");
StateView.SetStateKey(stateViews[1], "Success");

var layout = new VerticalStackLayout()
{
    Children =
    {
        new Label() { Text = "Default Content" }
    }
};

layout.SetBinding(StateContainer.CurrentStateProperty, "MyCurrentState");
StateContainer.SetStateViews(layout, stateViews);

Content = layout;
```

> [!IMPORTANT]
> The preceding examples assume a user-defined `MyCurrentState` string property is present in either a viewmodel or code-behind in order to determine the active state.

## Properties

### StateContainer

The StateContainer properties can be used on any `Layout` inheriting element.

| Property | Type | Description |
|--------------------------|-------------|--------------------------------------------------------------------------------------|
| StateViews | `IList<View>` | The available `View` elements to be used as state templates. |
| CurrentState | `string` | Determines which `View` element with the corresponding `StateKey` should be displayed. |
| ShouldAnimateOnStateChange | `bool` | Specifies if a fade out/in animation should display when switching between states. |

### StateView

The StateView properties can be used on any `View` inheriting element.

| Property | Type | Description |
|--------|--------|------------------|
| StateKey | `string` | Name of the state. |

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Layouts/).

## API

You can find the source code for `StateContainer` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/tree/main/src/CommunityToolkit.Maui/Layouts/StateContainer).
