---
title: ByteArrayToImageSourceConverter - .NET MAUI Community Toolkit
author: bijington
description: "The ByteArrayToImageSourceConverter is a converter that allows the user to convert an incoming value from a byte array and returns an ImageSource."
ms.date: 04/15/2022
---

# ByteArrayToImageSourceConverter

The `ByteArrayToImageSourceConverter` is a converter that allows the user to convert an incoming value from a `byte` array and returns an `ImageSource`. This object can then be used as the `Source` of an `Image` control.

The `Convert` method returns the supplied `byte[]` `value` converted to an `ImageSource`.

The `ConvertBack` method returns the supplied `ImageSource` `value` converted to a `byte[]`.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the ByteArrayToImageSourceConverter

The `ByteArrayToImageSourceConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.ByteArrayToImageSourceConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:ByteArrayToImageSourceConverter x:Key="ByteArrayToImageSourceConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Image Source="{Binding DotNetBotImageByteArray, Mode=OneWay, Converter={StaticResource ByteArrayToImageSourceConverter}}" />

</ContentPage>
```

### C#

The `ByteArrayToImageSourceConverter` can be used as follows in C#:

```csharp
class ByteArrayToImageSourceConverterPage : ContentPage
{
    public ByteArrayToImageSourceConverterPage()
    {
        var image = new Image();

	image.SetBinding(
		Image.SourceProperty,
		new Binding(
			nameof(ViewModel.DotNetBotImageByteArray),
			mode: BindingMode.OneWay,
			converter: new ByteArrayToImageSourceConverter()));

	Content = image;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class ByteArrayToImageSourceConverterPage : ContentPage
{
    public ByteArrayToImageSourceConverterPage()
    {
        Content = new Image()
            .Bind(
                Image.SourceProperty,
                static (ViewModel vm) => vm.DotNetBotImageByteArray,
                mode: BindingMode.OneWay,
                converter: new ByteArrayToImageSourceConverter());
    }
}
```

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/ByteArrayToImageSourceConverterPage.xaml).

## API

You can find the source code for `ByteArrayToImageSourceConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/ByteArrayToImageSourceConverter.shared.cs).
