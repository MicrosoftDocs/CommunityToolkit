---
title: StringToListConverter - .NET MAUI Community Toolkit
author: bijington
description: "The StringToListConverter is a one way converter that returns a set of substrings by splitting the input string based on one or more separators."
ms.date: 03/30/2022
---

# StringToListConverter

The `StringToListConverter` is a one way converter that returns a set of substrings by splitting the input string based on one or more separators.

The `Convert` method returns a set of substrings by splitting the input string based on one or more separators.

> [!NOTE]
> Note that the separators can be supplied in the following order of precedence:
> 1. as the `ConverterParameter` in the converter binding; this supersedes both `Separators` and `Separator` properties
> 2. as the `Separators` property on the converter; this supersedes the `Separator` property
> 3. as the `Separator` property on the converter.

The `ConvertBack` method is not supported. For the opposite behavior see the [`ListToStringConverter`](list-to-string-converter.md).

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the StringToListConverter

The `StringToListConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.StringToListConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
             <toolkit:StringToListConverter x:Key="StringToListConverter" SplitOptions="RemoveEmptyEntries">
                <toolkit:StringToListConverter.Separators>
                    <x:String>,</x:String>
                    <x:String>.</x:String>
                    <x:String>;</x:String>
                </toolkit:StringToListConverter.Separators>
            </toolkit:StringToListConverter>
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout>
        <Entry
            Placeholder="Enter some text separated by ',' or '.' or ';'"
            Text="{Binding MyValue}" />

        <CollectionView ItemsSource="{Binding MyValue, Converter={StaticResource StringToListConverter}}">
            <CollectionView.ItemTemplate>
                <DataTemplate>
                    <Label Text="{Binding .}" />
                </DataTemplate>
            </CollectionView.ItemTemplate>
        </CollectionView>
    </VerticalStackLayout>

</ContentPage>
```

### C#

The `StringToListConverter` can be used as follows in C#:

```csharp
class StringToListConverterPage : ContentPage
{
    public StringToListConverterPage()
    {
		var entry = new Entry { Placeholder = "Enter some text separated by ',' or '.' or ';'" };
		entry.SetBinding(Entry.TextProperty, new Binding(nameof(ViewModel.MyValue)));

		var stringToListConverter = new StringToListConverter
		{
			SplitOptions = System.StringSplitOptions.RemoveEmptyEntries,
			Separators = new [] { ",", ".", ";" }
		};

		var collectionView = new CollectionView
		{
			ItemTemplate = new DataTemplate(() =>
			{
				var itemLabel = new Label();
				itemLabel.SetBinding(Label.TextProperty, path: ".");
				return itemLabel;
			})
		};

		collectionView.SetBinding(
			CollectionView.ItemsSourceProperty,
			new Binding(
				nameof(ViewModel.MyValue),
				converter: stringToListConverter));

		Content = new VerticalStackLayout
        {
            Children =    
            {
                entry,
                collectionView
            }
        };
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class StringToListConverterPage : ContentPage
{
    public StringToListConverterPage()
    {
        Content = new VerticalStackLayout
        {
            Children =    
            {
                new Entry { Placeholder = "Enter some text separated by ',' or '.' or ';'" }
                    .Bind(
                        Entry.TextProperty, 
                        static (ViewModel vm) => vm.MyValue),

                new CollectionView
                {
                    ItemTemplate = new DataTemplate(() => new Label().Bind(Label.TextProperty, path: Binding.SelfPath))
                }.Bind(
                    CollectionView.ItemsSourceProperty,
                    static (ViewModel vm) => vm.MyValue,
                    converter: new StringToListConverter
                    {
                        SplitOptions = System.StringSplitOptions.RemoveEmptyEntries,
                        Separators = new [] { ",", ".", ";" }
                    })
            }
        };
    }
}
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| Separator | `string` | The string that delimits the substrings in the incoming string. This value is superseded by both `ConverterParameter` and `Separators`. If `ConverterParameter` is `null` and `Separators` is empty, this value will be used.  |
| Separators | `IList<string>` | The strings that delimits the substrings in the incoming string. This value is superseded by `ConverterParameter`. If `ConverterParameter` is `null` this value will be used. |
| SplitOptions | `StringSplitOptions` | A bitwise combination of the enumeration values that specifies whether to trim substrings and include empty substrings. |

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Converters/StringToListConverterPage.xaml).

## API

You can find the source code for `StringToListConverter` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/StringToListConverter.shared.cs).
