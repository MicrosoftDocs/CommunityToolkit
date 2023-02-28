---
title: EmailValidationBehavior - .NET MAUI Community Toolkit
author: bijington
description: "The EmailValidationBehavior is a Behavior that allows users to determine whether or not text input is a valid e-mail address."
ms.date: 04/20/2022
---

# EmailValidationBehavior

The `EmailValidationBehavior` is a `Behavior` that allows users to determine whether or not text input is a valid e-mail address. For example, an `Entry` control can be styled differently depending on whether a valid or an invalid e-mail address is provided. The validation is achieved through a regular expression that is used to verify whether or not the text input is a valid e-mail address.

When attached to an `InputView` (e.g. `Entry`, `Editor`, etc.), `EmailValidationBehavior` will change the default Keyboard, `Keyboard.Default`, to `Keyboard.Email`. If a non-default `Keyboard` has been specified for the `InputView`, `EmailValidationBehavior` will not change the `Keyboard`.

When detached from an `InputView`, `EmailValidationBehavior` will change `Keyboard.Email` back to `Keyboard.Default`. If a `Keyboard` other than `Keyboard.Email` has been specified for the `InputView`, `EmailValidationBehavior`, will not change the `Keyboard` when detaching.

## Syntax

The following examples show how to add the `EmailValidationBehavior` to an `Entry` and change the `TextColor` based on whether the entered text is a valid email address.

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the EmailValidationBehavior

The `EmailValidationBehavior` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Behaviors.EmailValidationBehaviorPage">

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
            <toolkit:EmailValidationBehavior 
                InvalidStyle="{StaticResource InvalidEntryStyle}"
                ValidStyle="{StaticResource ValidEntryStyle}"
                Flags="ValidateOnValueChanged" />
        </Entry.Behaviors>
    </Entry>

</ContentPage>
```

### C#

The `EmailValidationBehavior` can be used as follows in C#:

```csharp
class EmailValidationBehaviorPage : ContentPage
{
    public EmailValidationBehaviorPage()
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

        var emailValidationBehavior = new EmailValidationBehavior
        {
            InvalidStyle = invalidStyle,
            ValidStyle = validStyle,
            Flags = ValidationFlags.ValidateOnValueChanged
        };

        entry.Behaviors.Add(emailValidationBehavior);

        Content = entry;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a much more concise way to use this `Behavior` in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class EmailValidationBehaviorPage : ContentPage
{
    public EmailValidationBehaviorPage()
    {
        Content = new Entry()
            .Behaviors(new EmailValidationBehavior
            {
                InvalidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Red),
                ValidStyle = new Style<Entry>(Entry.TextColorProperty, Colors.Green),
                Flags = ValidationFlags.ValidateOnValueChanged
            });
    }
}
```

The following screenshot shows the resulting EmailValidationBehavior on Android:
![Screenshot of an EmailValidationBehavior on Android](../images/behaviors/email-validation-behavior-android.gif "EmailValidationBehavior on Android")

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| `DecorationFlags` | `TextDecorationFlags` | Provides enumerated value to use to set how to handle white spaces. |
| `MaximumLength` | `int` | The maximum length of the value that will be allowed. |
| `MinimumLength` | `int` | The minimum length of the value that will be allowed. |
| `RegexOptions` | `RegexOptions` | Provides enumerated values to use to set regular expression options. |
| `RegexPattern` | `string` | The regular expression pattern which the value will have to match before it will be allowed. |

[!INCLUDE [common validation properties](../includes/validation-behavior.md)]

## Methods

| Method  |Description  |
|---------|---------|
| EmailRegex (static) | A `GeneratedRegex` to match an input is a valid email address. |
| EmailDomainRegex (static) | A `GeneratedRegex` to match the domain of an email address. |

## Examples

You can find an example of this behavior in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Behaviors/EmailValidationBehaviorPage.xaml).

## API

You can find the source code for `EmailValidationBehavior` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Behaviors/Validators/EmailValidationBehavior.shared.cs).