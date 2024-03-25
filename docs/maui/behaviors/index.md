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
| [`CharactersValidationBehavior`](characters-validation-behavior.md) | The `CharactersValidationBehavior` is a `Behavior` that allows the user to validate text input depending on specified parameters. |
| [`EmailValidationBehavior`](email-validation-behavior.md) | The `EmailValidationBehavior` is a `Behavior` that allows users to determine whether or not text input is a valid e-mail address. |
| [`EventToCommandBehavior`](event-to-command-behavior.md) | The `EventToCommandBehavior` is a `behavior` that allows the user to invoke a `Command` through an `Event`. It is designed to associate Commands to events exposed by controls that were not designed to support Commands. It allows you to map any arbitrary event on a control to a Command. |
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
