---
title: Expander - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The Expander allows collapse and expand content."
ms.date: 11/08/2022
---

# Expander

The `Expander` control provides an expandable container to host any content. The control has a header and content, and the content is shown or hidden by tapping the `Expander` header. When only the `Expander` header is shown, the `Expander` is *collapsed*. When the `Expander` content is visible the `Expander` is *expanded*.

> [!NOTE]
> The `Expander` control is known to show unwanted behavior when used in a `ListView` on iOS/MacCatalyst or `CollectionView` on Windows.

![Screenshot of an Expander in collapsed and expanded states](../images/views/Expander.gif "Expander on Android")

## Basic usage

The following example shows how to instantiate an `Expander`.

### XAML

```xml
<Expander>
    <Expander.Header>
        <Label Text="Baboon"
               FontAttributes="Bold"
               FontSize="Medium" />
    </Expander.Header>
    <Grid Padding="10">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="Auto" />
            <ColumnDefinition Width="Auto" />
        </Grid.ColumnDefinitions>
        <Image Source="http://upload.wikimedia.org/wikipedia/commons/thumb/f/fc/Papio_anubis_%28Serengeti%2C_2009%29.jpg/200px-Papio_anubis_%28Serengeti%2C_2009%29.jpg"
               Aspect="AspectFill"
               HeightRequest="120"
               WidthRequest="120" />
        <Label Grid.Column="1"
               Text="Baboons are African and Arabian Old World monkeys belonging to the genus Papio, part of the subfamily Cercopithecinae."
               FontAttributes="Italic" />
    </Grid>
</Expander>
```

### C#

```csharp
using CommunityToolkit.Maui.Views;

var expander = new Expander
{
    Header = new Label
    {
        Text = "Baboon",
        FontAttributes = FontAttributes.Bold,
        FontSize = Device.GetNamedSize(NamedSize.Medium, typeof(Label))
    }
};

var grid = new Grid
{
    Padding = new Thickness(10),
    ColumnDefinitions =
    {
        new ColumnDefinition { Width = GridLength.Auto },
        new ColumnDefinition { Width = GridLength.Auto }
    }
};

grid.Children.Add(new Image
{
    Source = "http://upload.wikimedia.org/wikipedia/commons/thumb/f/fc/Papio_anubis_%28Serengeti%2C_2009%29.jpg/200px-Papio_anubis_%28Serengeti%2C_2009%29.jpg",
    Aspect = Aspect.AspectFill,
    HeightRequest = 120,
    WidthRequest = 120
});

grid.Children.Add(new Label
{
    Text = "Baboons are African and Arabian Old World monkeys belonging to the genus Papio, part of the subfamily Cercopithecinae.",
    FontAttributes = FontAttributes.Italic
}, 1, 0);

expander.Content = grid;
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
`Command` | `ICommand` | Executes when the `Expander` header is tapped.
`CommandParameter` | `object` | The parameter that's passed to the `Command`.
`Direction` | `ExpandDirection` | Defines the expander direction.
`Content` | `View` | Defines the content to be displayed when the `Expander` expands.
`Header` | `IView` | Defines the header content.
`IsExpanded` | `bool` | Determines if the `Expander` is expanded. This property uses the `TwoWay` binding mode, and has a default value of `false`.

The `ExpandDirection` enumeration defines the following members:

|Value  |Description  |
|---------|---------|
`Down` | Indicates that the `Expander` content is under the header.
`Up` | Indicates that the `Expander` content is above the header.

The `Expander` control also defines a `ExpandedChanged` event that's fired when the `Expander` header is tapped.

### ExpandedChangedEventArgs

Event argument which contains `Expander` `IsExpanded` state.

#### Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| IsExpanded | `bool` | Determines if the `Expander` is expanded. |

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/ExpanderPage.xaml.cs).

## API

You can find the source code for `Expander` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Views/Expander).
