---
title: Behaviors - .NET MAUI Community Toolkit
author: bijington
description: The .NET MAUI Community Toolkit provides a collection of pre-built, reusable behaviors to make developers lives easier.
ms.date: 03/30/2022
---

# .NET MAUI Behaviors

.NET Multi-platform App UI (.NET MAUI) behaviors let you add functionality to user interface controls without having to subclass them. Instead, the functionality is implemented in a behavior class and attached to the control as if it was part of the control itself.

For further information on Behaviors please refer to the [.NET MAUI documentation](/dotnet/maui/fundamentals/behaviors).

## .NET MAUI Community Toolkit Behaviors

The .NET MAUI Community Toolkit provides a collection of pre-built, reusable behaviors to make developers lives easier. Here are the behaviors provided by the toolkit:

| Behavior | Description |
| --------- | ----------- |
| [`AnimationBehavior`](animation-behavior.md) | The `AnimationBehavior` is a `Behavior` that provides the ability to animate any `VisualElement` it is attached to. |
| [`CharactersValidationBehavior`](characters-validation-behavior.md) | The `CharactersValidationBehavior` is a `Behavior` that allows the user to validate text input depending on specified parameters. |
| [`EmailValidationBehavior`](email-validation-behavior.md) | The `EmailValidationBehavior` is a `Behavior` that allows users to determine whether or not text input is a valid e-mail address. |
| [`EventToCommandBehavior`](event-to-command-behavior.md) | The `EventToCommandBehavior` is a `behavior` that allows the user to invoke a `Command` through an `Event`. It is designed to associate Commands to events exposed by controls that were not designed to support Commands. It allows you to map any arbitrary event on a control to a Command. |
| [`IconTintColorBehavior`](icon-tint-color-behavior.md) | The `IconTintColorBehavior` is a `behavior` that allows you to tint an image. |
| [`ImageTouchBehavior`](image-touch-behavior.md) | The `ImageTouchBehavior` extends the `TouchBehavior` by providing the ability to customize `Image` elements based on touch, mouse click and hover events. |
| [`MaskedBehavior`](masked-behavior.md) | The `MaskedBehavior` is a `Behavior` that allows the user to define an input mask for data entry. |
| [`MaxLengthReachedBehavior`](maximum-length-reached-behavior.md) | The `MaxLengthReachedBehavior` is a behavior that allows the user to trigger an action when a user has reached the maximum length allowed on an `InputView`. |
| [`MultiValidationBehavior`](multi-validation-behavior.md) | The `MultiValidationBehavior` is a `Behavior` that allows the user to combine multiple validators to validate text input depending on specified parameters. |
| [`NumericValidationBehavior`](numeric-validation-behavior.md) | The `NumericValidationBehavior` is a `Behavior` that allows the user to determine if text input is a valid numeric value. |
| [`ProgressBarAnimationBehavior`](progressbar-animation-behavior.md) | The `ProgressBarAnimationBehavior` animates a `ProgressBar` from its current Progress value to a provided value over time. |
| [`RequiredStringValidationBehavior`](required-string-validation-behavior.md) | The `RequiredStringValidationBehavior` is a `Behavior` that allows the user to determine if text input is equal to specific text. |
| [`SelectAllTextBehavior`](select-all-text-behavior.md) | The `SelectAllTextBehavior` is a `Behavior` that allows selecting all text in an `InputView` (e.g. an `Entry` or `Editor`) when it becomes focused.
| [`SetFocusOnEntryCompletedBehavior`](set-focus-when-entry-completed-behavior.md) | The `SetFocusOnEntryCompletedBehavior` is a `Behavior` that gives focus to a specified `VisualElement` when an `Entry` is completed. |
| [`StatusBarBehavior`](statusbar-behavior.md) | The `StatusBarBehavior` is a `Behavior` that allows you to customize the color and style of your device statusbar.|
| [`TextValidationBehavior`](text-validation-behavior.md) | The `TextValidationBehavior` is a `Behavior` that allows the user to validate a given text depending on specified parameters. |
| [`TouchBehavior`](touch-behavior.md) | The `TouchBehavior` is a `Behavior` that provides the ability to interact with any `VisualElement` based on touch, mouse click and hover events. |
| [`UriValidationBehavior`](uri-validation-behavior.md) | The `UriValidationBehavior` is a `Behavior` that allows users to determine whether or not text input is a valid URI. |
| [`UserStoppedTypingBehavior`](user-stopped-typing-behavior.md) | The `UserStoppedTypingBehavior` is a behavior that allows the user to trigger an action when a user has stopped data input an `Entry`. |

## Create a .NET MAUI Community Toolkit Behavior

The .NET MAUI Community Toolkit provides the `BaseBehavior<T>` class that performs some of the boiler plate requirements around managing a `Behavior` enabling developers to focus on the purpose of the implementation. A .NET MAUI Community Toolkit behavior can be implemented by creating a class that derives from the `BaseBehavior<T>` class, and optionally overriding the `OnAttachedTo`, `OnDetachingFrom` or `OnViewPropertyChanged` methods.

The following example shows the `NumericValidationBehavior` class, which highlights the value entered by the user into an `Entry` control in red if it's not a `double`:

```csharp
public class NumericValidationBehavior : Behavior<Entry>
{
    void OnViewPropertyChanged(Entry sender, PropertyChangedEventArgs e)
    {
        if (e.PropertyName == nameof(Entry.Text))
        {
            bool isValid = double.TryParse(sender.Text, out double _);
            sender.TextColor = isValid ? Colors.Black : Colors.Red;
        }
    }
}
```

In this example, the `NumericValidationBehavior` class derives from the `BaseBehavior<T>` class, where `T` is an `Entry`. The `OnAttachedTo` and `OnDetachingFrom` methods are handled within the base implementation so the only requirement is to override the `OnViewPropertyChanged`. The `OnViewPropertyChanged` method will be called whenever a property changes on the `View` property which is of `Entry`. This `OnViewPropertyChanged` provides the core functionality of the behavior, which parses the value entered in the `Entry` and sets the `TextColor` property to red if the value isn't a `double`.
