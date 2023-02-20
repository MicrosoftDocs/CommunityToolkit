---
title: CharactersValidationBehavior - .NET MAUI Community Toolkit
author: bijington
description: "The CharactersValidationBehavior is a Behavior that allows the user to validate text input depending on specified parameters."
ms.date: 04/20/2022
---

# CharactersValidationBehavior

The `CharactersValidationBehavior` is a `Behavior` that allows the user to validate text input depending on specified parameters. For example, an `Entry` control can be styled differently depending on whether a valid or an invalid text value is provided. This behavior includes built-in checks such as checking for a certain number of digits or alphanumeric characters. 

## Syntax

The following examples show how to add the `CharactersValidationBehavior` to an `Entry` and change the `TextColor` based on whether the entered text only contains numbers and have at least 2 numbers.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the CharactersValidationBehavior

The `CharactersValidationBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Behaviors.CharactersValidationBehaviorPage">

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
            <toolkit:CharactersValidationBehavior 
                InvalidStyle="{StaticResource InvalidEntryStyle}"
                ValidStyle="{StaticResource ValidEntryStyle}"
                Flags="ValidateOnValueChanged"
                CharacterType="Digit"
                MinimumCharacterTypeCount="3" />
        </Entry.Behaviors>
    </Entry>

</ContentPage>
```

### C#

The `CharactersValidationBehavior` can be used as follows in C#:

```csharp
class CharactersValidationBehaviorPage : ContentPage
{
    public CharactersValidationBehaviorPage()
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

        var charactersValidationBehavior = new CharactersValidationBehavior
        {
            InvalidStyle = invalidStyle,
            ValidStyle = validStyle,
            Flags = ValidationFlags.ValidateOnValueChanged,
            CharacterType = CharacterType.Digit,
            MinimumCharacterTypeCount = 3
        };

        entry.Behaviors.Add(charactersValidationBehavior);

        Content = entry;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class CharactersValidationBehaviorPage : ContentPage
{
    public CharactersValidationBehaviorPage()
    {
        Content = new Entry()
            .Behaviors(new CharactersValidationBehavior
            {
                InvalidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Red),
                ValidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Green),
                Flags = ValidationFlags.ValidateOnValueChanged,
                CharacterType = CharacterType.Digit,
                MinimumCharacterTypeCount = 3
            });
    }
}
```

The following screenshot shows the resulting CharactersValidationBehavior on Android:
![Screenshot of an CharactersValidationBehavior on Android](../images/behaviors/character-validation-behavior-android.gif "CharactersValidationBehavior on Android")

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| `CharacterType` | `CharacterType` | Provides an enumerated value to use to set how to handle comparisons. |
| `DecorationFlags` | `TextDecorationFlags` | Provides enumerated value to use to set how to handle white spaces. |
| `MaximumCharacterTypeCount` | `int` | The maximum number of `CharacterType` characters required. |
| `MaximumLength` | `int` | The maximum length of the value that will be allowed. |
| `MinimumCharacterTypeCount` | `int` | The minimum number of `CharacterType` characters required. |
| `MinimumLength` | `int` | The minimum length of the value that will be allowed. |
| `RegexOptions` | `RegexOptions` | Provides enumerated values to use to set regular expression options. |
| `RegexPattern` | `string` | The regular expression pattern which the value will have to match before it will be allowed. |

[!INCLUDE [common validation properties](../includes/validation-behavior.md)]

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/CharactersValidationBehaviorPage.xaml).

## API

You can find the source code for `CharactersValidationBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/Validators/CharactersValidationBehavior.shared.cs).