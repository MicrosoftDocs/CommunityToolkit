---
title: TextValidationBehavior - .NET MAUI Community Toolkit
author: bijington
description: "The TextValidationBehavior is a Behavior that allows the user to validate a given text depending on specified parameters."
ms.date: 04/20/2022
---

# TextValidationBehavior

The `TextValidationBehavior` is a `Behavior` that allows the user to validate a given text depending on specified parameters. By adding this behavior to any `InputView` control it can be styled differently depending on whether a valid or an invalid text value is provided. It offers various built-in checks such as checking for a certain length or whether or not the input value matches a specific regular expression.

## Syntax

The following examples show how to add the `TextValidationBehavior` to an `Entry` and change the `TextColor` based on whether the entered text is between 1 and 10 characters long.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the TextValidationBehavior

The `TextValidationBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Behaviors.TextValidationBehaviorPage">

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
            <toolkit:TextValidationBehavior 
                InvalidStyle="{StaticResource InvalidEntryStyle}"
                ValidStyle="{StaticResource ValidEntryStyle}"
                Flags="ValidateOnValueChanged"
                MinimumLength="1"
                MaximumLength="10" />
        </Entry.Behaviors>
    </Entry>

</ContentPage>
```

### C#

The `TextValidationBehavior` can be used as follows in C#:

```csharp
class TextValidationBehaviorPage : ContentPage
{
    public TextValidationBehaviorPage()
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

        var textValidationBehavior = new TextValidationBehavior
        {
            InvalidStyle = invalidStyle,
            ValidStyle = validStyle,
            Flags = ValidationFlags.ValidateOnValueChanged,
            MinimumLength = 1,
            MaximumLength = 10
        };

        entry.Behaviors.Add(textValidationBehavior);

        Content = entry;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class TextValidationBehaviorPage : ContentPage
{
    public TextValidationBehaviorPage()
    {
        Content = new Entry()
            .Behaviors(new TextValidationBehavior
            {
                InvalidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Red),
                ValidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Green),
                Flags = ValidationFlags.ValidateOnValueChanged,
                MinimumLength = 1,
                MaximumLength = 10
            });
    }
}
```

The following screenshot shows the resulting TextValidationBehavior on Android:
![Screenshot of an TextValidationBehavior on Android](../images/behaviors/text-validation-behavior-android.gif "TextValidationBehavior on Android")

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| `DecorationFlags` | `TextDecorationFlags` | Provides enumerated value to use to set how to handle white spaces. |
| `MaximumLength` | `int` | The maximum length of the value that will be allowed. |
| `MinimumLength` | `int` | The minimum length of the value that will be allowed. |
| `RegexOptions` | `RegexOptions` | Provides enumerated values to use to set regular expression options. |
| `RegexPattern` | `string` | The regular expression pattern which the value will have to match before it will be allowed. |

[!INCLUDE [common validation properties](../includes/validation-behavior.md)]

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/TextValidationBehaviorPage.xaml).

## API

You can find the source code for `TextValidationBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/Validators/TextValidationBehavior.shared.cs).
