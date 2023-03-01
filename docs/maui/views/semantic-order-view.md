---
title: SemanticOrderView - .NET MAUI Community Toolkit
author: bijington
description: The SemanticOrderView provides the ability to control the order of VisualElements for screen readers and improve the Accessibility of an application.
ms.date: 02/28/2023
---

The `SemanticOrderView` provides the ability to control the order of VisualElements for screen readers and improve the Accessibility of an application. This can be particularly useful when building user interfaces in orders differing from the order in which users and screen readers will navigate them.

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
                
                <Label x:Name="DescriptionLabel" Text="{Binding Description}">

                <Label x:Name="TitleLabel" Text="{Binding Title}" FontSize="30">

            </Grid>
        </toolkit:SemanticOrderView>
    </ContentPage.Content>
</ContentPage>
```

To over come that, in the code behind file we can change the order that will be used by the device's screen reader as follows:

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

## Examples

You can find an example of this feature in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/SemanticOrderView/).

## API

You can find the source code for `SemanticOrderView` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/tree/main/src/CommunityToolkit.Maui/Views/SemanticOrderView).
