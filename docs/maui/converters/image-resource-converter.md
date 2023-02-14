---
title: ImageResourceConverter - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The ImageResourceConverter is a converter that converts embedded image resource ID to its ImageSource."
ms.date: 05/04/2022
---

# ImageResourceConverter

The `ImageResourceConverter` is a converter that converts embedded image resource ID to its ImageSource. An embedded image resource is when an image has been added to a project with the **Build Action** set to **Embedded Resource**. It's ID is it's fully qualified name; so the namespace of the project + the resource name. In the example of a project named `CommunityToolkit.Maui.Sample`, a set of nested folders of `Resources/Embedded` and an image named `dotnetbot.png` the ID would be generated with:

`CommunityToolkit.Maui.Sample` + `Resources.Embedded` + `dotnetbot.png`

which results in:

`CommunityToolkit.Maui.Sample.Resources.Embedded.dotnetbot.png`

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ImageResourceConverter

The `ImageResourceConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ImageResourceConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ImageResourceConverter x:Key="ImageResourceConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Image Source="{Binding MyImageResource, Converter={StaticResource ImageResourceConverter}}" />

</ContentPage>
```

### C#

The `ImageResourceConverter` can be used as follows in C#:

```csharp
class ImageResourceConverterPage : ContentPage
{
    public ImageResourceConverterPage()
    {
        var image = new Image();

        image.SetBinding(
            Image.SourceProperty, 
            new Binding(
                nameof(ViewModel.MyImageResource), 
                converter: new ImageResourceConverter())); 

        Content = label;        
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class ImageResourceConverterPage : ContentPage
{
    public ImageResourceConverterPage()
    {
        Content = new Image()
            .Bind(
                Label.SourceProperty, 
                static (ViewModel vm) => vm.MyImageResource,
                converter: new ImageResourceConverter()); 
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ImageResourceConverterPage.xaml).

## API

You can find the source code for `ImageResourceConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ImageResourceConverter.shared.cs).
