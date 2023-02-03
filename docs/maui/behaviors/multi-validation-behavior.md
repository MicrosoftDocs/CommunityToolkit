---
title: MultiValidationBehavior - .NET MAUI Community Toolkit
author: bijington
description: "The MultiValidationBehavior is a Behavior that allows the user to validate a given text depending on specified parameters."
ms.date: 05/18/2022
---

# MultiValidationBehavior

The `MultiValidationBehavior` is a `Behavior` that allows the user to combine multiple validators to validate text input depending on specified parameters. For example, an `Entry` control can be styled differently depending on whether a valid or an invalid text input is provided. By allowing the user to chain multiple existing validators together, it offers a high degree of customization when it comes to validation.

## Syntax

The following examples show how to add the `MultiValidationBehavior` to an `Entry` and include 4 different validation behaviors to enforce a password policy.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the MultiValidationBehavior

The `MultiValidationBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Behaviors.MultiValidationBehaviorPage">

    <ContentPage.Resources>
        <Style x:Key="InvalidEntryStyle" TargetType="Entry">
            <Setter Property="TextColor" Value="Red" />
        </Style>
        <Style x:Key="ValidEntryStyle" TargetType="Entry">
            <Setter Property="TextColor" Value="Green" />
        </Style>
    </ContentPage.Resources>

    <Entry 
        IsPassword="True"
        Placeholder="Password">

        <Entry.Behaviors>
            <toolkit:MultiValidationBehavior 
                InvalidStyle="{StaticResource InvalidEntryStyle}"  
                ValidStyle="{StaticResource ValidEntryStyle}"
                Flags="ValidateOnValueChanged">

                <toolkit:CharactersValidationBehavior 
                    x:Name="DigitValidation" 
                    CharacterType="Digit" 
                    MinimumCharacterTypeCount="1" 
                    toolkit:MultiValidationBehavior.Error="1 digit" 
                    RegexPattern="" />

                <toolkit:CharactersValidationBehavior 
                    x:Name="UpperValidation" 
                    CharacterType="UppercaseLetter" 
                    MinimumCharacterTypeCount="1" 
                    toolkit:MultiValidationBehavior.Error="1 upper case" 
                    RegexPattern="" />

                <toolkit:CharactersValidationBehavior 
                    x:Name="SymbolValidation" 
                    CharacterType="NonAlphanumericSymbol" 
                    MinimumCharacterTypeCount="1" 
                    toolkit:MultiValidationBehavior.Error="1 symbol" 
                    RegexPattern=""  />

                <toolkit:CharactersValidationBehavior 
                    x:Name="AnyValidation" 
                    CharacterType="Any" 
                    MinimumCharacterTypeCount="8" 
                    toolkit:MultiValidationBehavior.Error="8 characters" 
                    RegexPattern="" />
            </toolkit:MultiValidationBehavior>
        </Entry.Behaviors>
    </Entry>

</ContentPage>
```

### C#

The `MultiValidationBehavior` can be used as follows in C#:

```csharp
class MultiValidationBehaviorPage : ContentPage
{
    public MultiValidationBehaviorPage()
    {
        var entry = new Entry
        {
            IsPassword = true,
            Placeholder = "Password"
        };

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

        var atLeastOneDigit = new CharactersValidationBehavior
        {
            Flags = ValidationFlags.ValidateOnValueChanged,
            CharacterType = CharacterType.Digit,
            MinimumCharacterCount = 1    
        };

        MultiValidationBehavior.SetError(atLeastOneDigit, "1 digit");

        var atLeastUpperCase = new CharactersValidationBehavior
        {
            Flags = ValidationFlags.ValidateOnValueChanged,
            CharacterType = CharacterType.UppercaseLetter,
            MinimumCharacterCount = 1    
        };

        MultiValidationBehavior.SetError(atLeastUpperCase, "1 upper case");

        var atLeastOneSymbol = new CharactersValidationBehavior
        {
            Flags = ValidationFlags.ValidateOnValueChanged,
            CharacterType = CharacterType.NonAlphanumericSymbol,
            MinimumCharacterCount = 1    
        };

        MultiValidationBehavior.SetError(atLeastOneSymbol, "1 symbol");

        var atLeastEightCharacters = new CharactersValidationBehavior
        {
            Flags = ValidationFlags.ValidateOnValueChanged,
            CharacterType = CharacterType.Any,
            MinimumCharacterCount = 1    
        };

        MultiValidationBehavior.SetError(atLeastEightCharacters, "8 characters");

        var multiValidationBehavior = new MultiValidationBehavior
        {
            InvalidStyle = invalidStyle,
            ValidStyle = validStyle,
            Flags = ValidationFlags.ValidateOnValueChanged,

            Children = 
            {
                atLeastOneDigit,
                atLeastUpperCase,
                atLeastOneSymbol,
                atLeastEightCharacters
            }
        };

        entry.Behaviors.Add(multiValidationBehavior);

        Content = entry;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class MultiValidationBehaviorPage : ContentPage
{
    public MultiValidationBehaviorPage()
    {
        Content = new Entry()
            .Behaviors(new MultiValidationBehavior
            {
                InvalidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Red),
                ValidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Green),
                Flags = ValidationFlags.ValidateOnValueChanged,

                Children = 
                {
                    new CharactersValidationBehavior
                    {
                        Flags = ValidationFlags.ValidateOnValueChanged,
                        CharacterType = CharacterType.Digit,
                        MinimumCharacterCount = 1    
                    }
                    .Assign(out var atLeastOneDigit),

                    new CharactersValidationBehavior
                    {
                        Flags = ValidationFlags.ValidateOnValueChanged,
                        CharacterType = CharacterType.UppercaseLetter,
                        MinimumCharacterCount = 1    
                    }
                    .Assign(out var atLeastUpperCase),

                    new CharactersValidationBehavior
                    {
                        Flags = ValidationFlags.ValidateOnValueChanged,
                        CharacterType = CharacterType.NonAlphanumericSymbol,
                        MinimumCharacterCount = 1    
                    }
                    .Assign(out var atLeastOneSymbol),

                    new CharactersValidationBehavior
                    {
                        Flags = ValidationFlags.ValidateOnValueChanged,
                        CharacterType = CharacterType.Any,
                        MinimumCharacterCount = 8  
                    }
                    .Assign(out var atLeastEightCharacters),
                }
            });

        MultiValidationBehavior.SetError(atLeastOneDigit, "1 digit");
        MultiValidationBehavior.SetError(atLeastUpperCase, "1 upper case");
        MultiValidationBehavior.SetError(atLeastOneSymbol, "1 symbol");
        MultiValidationBehavior.SetError(atLeastEightCharacters, "8 characters");
    }
}
```

The following screenshot shows the resulting MultiValidationBehavior on Android:
![Screenshot of an MultiValidationBehavior on Android](../images/behaviors/multi-validation-behavior-android.gif "MultiValidationBehavior on Android")

## Properties

The `MultiValidationBehavior` provides the common validation properties as below.

[!INCLUDE [common validation properties](../includes/validation-behavior.md)]

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/MultiValidationBehaviorPage.xaml).

## API

You can find the source code for `MultiValidationBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/MultiValidationBehavior.cs).