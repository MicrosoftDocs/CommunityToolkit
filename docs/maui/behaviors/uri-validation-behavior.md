---
title: UriValidationBehavior - .NET MAUI Community Toolkit
author: bijington
description: "The UriValidationBehavior is a Behavior that allows users to determine whether or not text input is a valid URI."
ms.date: 04/20/2022
---

# UriValidationBehavior

The `UriValidationBehavior` is a `Behavior` that allows users to determine whether or not text input is a valid URI. For example, an `Entry` control can be styled differently depending on whether a valid or an invalid URI is provided.

## Syntax

The following examples show how to add the `UriValidationBehavior` to an `Entry` and change the `TextColor` based on whether the entered text is a valid absolute URI.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the UriValidationBehavior

The `UriValidationBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Behaviors.UriValidationBehaviorPage">

    <ContentPage.Resources>
        <Style x:Key="InvalidEntryStyle" TargetType="Entry">
            <Setter Property="TextColor" Value="Red" />
        </Style>
        <Style x:Key="ValidEntryStyle" TargetType="Entry">
            <Setter Property="TextColor" Value="Green" />
        </Style>
    </ContentPage.Resources>

    <Entry>
        <Entry.Behaviors>
            <toolkit:UriValidationBehavior 
                InvalidStyle="{StaticResource InvalidEntryStyle}"
                ValidStyle="{StaticResource ValidEntryStyle}"
                Flags="ValidateOnValueChanged"
                UriKind="Absolute" />
        </Entry.Behaviors>
    </Entry>

</ContentPage>
```

### C#

The `UriValidationBehavior` can be used as follows in C#:

```csharp
class UriValidationBehaviorPage : ContentPage
{
    public UriValidationBehaviorPage()
    {
        var entry = new Entry();

        var validStyle = new Style(typeof(Entry));
        validStyle.Setters.Add(new Setter
        {
            Property = Entry.TextColorProperty,
            Value = Colors.Green
        });

        var invalidStyle = new Style(typeof(Entry));
        invalidStyle.Setters.Add(new Setter
        {
            Property = Entry.TextColorProperty,
            Value = Colors.Red
        });

        var uriValidationBehavior = new UriValidationBehavior
        {
            InvalidStyle = invalidStyle,
            ValidStyle = validStyle,
            Flags = ValidationFlags.ValidateOnValueChanged,
            UriKind = UriKind.Absolute
        };

        entry.Behaviors.Add(uriValidationBehavior);

        Content = entry;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class UriValidationBehaviorPage : ContentPage
{
    public UriValidationBehaviorPage()
    {
        Content = new Entry()
            .Behaviors(new UriValidationBehavior
            {
                InvalidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Red),
                ValidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Green),
                Flags = ValidationFlags.ValidateOnValueChanged,
                UriKind = UriKind.Absolute
            });
    }
}
```

The following screenshot shows the resulting UriValidationBehavior on Android:
![Screenshot of an UriValidationBehavior on Android](../images/behaviors/uri-validation-behavior-android.gif "UriValidationBehavior on Android")

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| `DecorationFlags` | `TextDecorationFlags` | Provides enumerated value to use to set how to handle white spaces. |
| `MaximumLength` | `int` | The maximum length of the value that will be allowed. |
| `MinimumLength` | `int` | The minimum length of the value that will be allowed. |
| `RegexOptions` | `RegexOptions` | Provides enumerated values to use to set regular expression options. |
| `RegexPattern` | `string` | The regular expression pattern which the value will have to match before it will be allowed. |
| `UriKind` | `UriKind` | Determines the type of URI to accept as valid. |

[!INCLUDE [common validation properties](../includes/validation-behavior.md)]

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/UriValidationBehaviorPage.xaml).

## API

You can find the source code for `UriValidationBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/Validators/UriValidationBehavior.shared.cs).