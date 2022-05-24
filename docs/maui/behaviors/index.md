---
title: Behaviors - .NET MAUI Community Toolkit
author: bijington
description: The .NET MAUI Community Toolkit provides a collection of pre-built, reusable behaviors to make developers lives easier.
ms.date: 03/30/2022
---

# Behaviors

.NET Multi-platform App UI (.NET MAUI) behaviors let you add functionality to user interface controls without having to subclass them. Instead, the functionality is implemented in a behavior class and attached to the control as if it was part of the control itself.

For further information on Behaviors please refer to the [.NET MAUI documentation](/dotnet/maui/fundamentals/behaviors).

## .NET MAUI Community Toolkit Behaviors

The .NET MAUI Community Toolkit provides a collection of pre-built, reusable behaviors to make developers lives easier. Here are the behaviors provided by the toolkit:

| Behavior | Description |
| --------- | ----------- |
| [`CharactersValidationBehavior`](characters-validation-behavior.md) | The `CharactersValidationBehavior` is a `Behavior` that allows the user to validate text input depending on specified parameters. |
| [`EmailValidationBehavior`](email-validation-behavior.md) | The `EmailValidationBehavior` is a `Behavior` that allows users to determine whether or not text input is a valid e-mail address. |
| [`EventToCommandBehavior`](event-to-command-behavior.md) | The `EventToCommandBehavior` is a `behavior` that allows the user to invoke a `Command` through an `Event`. It is designed to associate Commands to events exposed by controls that were not designed to support Commands. It allows you to map any arbitrary event on a control to a Command. |
| [`MaskedBehavior`](masked-behavior.md) | The `MaskedBehavior` is a `Behavior` that allows the user to define an input mask for data entry. |
| [`MaxLengthReachedBehavior`](maximum-length-reached-behavior.md) | The `MaxLengthReachedBehavior` is a behavior that allows the user to trigger an action when a user has reached the maximum length allowed on an `InputView`. |
| [`MultiValidationBehavior`](multi-validation-behavior.md) | The `MultiValidationBehavior` is a `Behavior` that allows the user to combine multiple validators to validate text input depending on specified parameters. |
| [`NumericValidationBehavior`](numeric-validation-behavior.md) | The `NumericValidationBehavior` is a `Behavior` that allows the user to determine if text input is a valid numeric value. |
| [`ProgressBarAnimationBehavior`](progressbar-animation-behavior.md) | The `ProgressBarAnimationBehavior` animates a `ProgressBar` from its current Progress value to a provided value over time. |
| [`RequiredStringValidationBehavior`](required-string-validation-behavior.md) | The `RequiredStringValidationBehavior` is a `Behavior` that allows the user to determine if text input is equal to specific text. |
| [`SetFocusOnEntryCompletedBehavior`](set-focus-when-entry-completed-behavior.md) | The `SetFocusOnEntryCompletedBehavior` is a `Behavior` that gives focus to a specified `VisualElement` when an `Entry` is completed. |
| [`TextValidationBehavior`](text-validation-behavior.md) | The `TextValidationBehavior` is a `Behavior` that allows the user to validate a given text depending on specified parameters. |
| [`UriValidationBehavior`](uri-validation-behavior.md) | The `UriValidationBehavior` is a `Behavior` that allows users to determine whether or not text input is a valid URI. |
| [`UserStoppedTypingBehavior`](user-stopped-typing-behavior.md) | The `UserStoppedTypingBehavior` is a behavior that allows the user to trigger an action when a user has stopped data input an `Entry`. |
