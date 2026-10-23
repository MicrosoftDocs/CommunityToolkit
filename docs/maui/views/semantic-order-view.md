---
title: SemanticOrderView - .NET MAUI Community Toolkit
author: bijington
description: The SemanticOrderView provides the ability to control the order of VisualElements for screen readers and improve the Accessibility of an application.
ms.date: 10/23/2026
---

# SemanticOrderView

The `SemanticOrderView` provides the ability to control the order of VisualElements for screen readers, and on Windows the keyboard Tab order, and improve the Accessibility of an application. This can be particularly useful when building user interfaces in orders differing from the order in which users and screen readers will navigate them.

## Using the SemanticOrderView

The following example shows how the `SemanticOrderView` can change the order in which the screen reader announces elements away from the order in which they are added to the user interface. The XAML below shows the `TitleLabel` rendering the title _after_ the `DescriptionLabel` that renders the description, this means that visually we will see the description before the title. While that might make sense when someone is looking at it, it doesn't necessarily make sense for someone who is visually impaired and doesn't see the screen (entirely).

```xaml
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
    x:Class="CommunityToolkit.Maui.Sample.Pages.Views.SemanticOrderViewPage"
    Title="Semantic Order View">
    <ContentPage.Content>
        <toolkit:SemanticOrderView x:Name="SemanticOrderView">
            <Grid RowDefinitions="2*,*">
                
                <Label x:Name="DescriptionLabel" Text="{Binding Description}" />

                <Label x:Name="TitleLabel" Text="{Binding Title}" FontSize="30" />

            </Grid>
        </toolkit:SemanticOrderView>
    </ContentPage.Content>
</ContentPage>
```

To overcome that, in the code behind file we can change the order that will be used by the device's screen reader as follows:

```csharp
using System.Collections.Generic;

namespace CommunityToolkit.Maui.Sample.Pages.Views;

public partial class SemanticOrderViewPage : ContentPage
{
    public SemanticOrderViewPage()
    {
        InitializeComponent();

        this.SemanticOrderView.ViewOrder = new List<View> { TitleLabel, DescriptionLabel };
    }
}
```

With this, we tell the `SemanticOrderView` that the "proper" order for these controls, when accessed through screen reader software, is to first focus the `TitleLabel` and then `DescriptionLabel`.

## Platform behavior

The views that aren't in `ViewOrder` stay accessible on every platform.

|Platform  |Behavior  |
|---------|---------|
| iOS and Mac Catalyst | The views of `ViewOrder` are the first accessibility elements of the `SemanticOrderView`, in that order. Assistive technologies visit the other views after them, in the order of the view hierarchy. |
| Android | On Android 5.1 (API 22) or later, the order of `ViewOrder` determines how TalkBack traverses the views. On earlier versions the order isn't applied, and a message is written to the trace output. |
| Windows | `ViewOrder` sets the keyboard Tab order of the views. It doesn't change the order in which Narrator reads them, which follows the visual tree. |

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/SemanticOrderView/).

## API

You can find the source code for `SemanticOrderView` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/tree/main/src/CommunityToolkit.Maui/Views/SemanticOrderView).
