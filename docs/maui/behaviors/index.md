---
title: Behaviors - .NET MAUI Community Toolkit
author: bijington
description: The .NET MAUI Community Toolkit provides a collection of pre-built, reusable behaviors to make developers lives easier.
ms.date: 03/30/2022
---

# Behaviors

[!INCLUDE [docs under construction](../includes/preview-note.md)]

.NET Multi-platform App UI (.NET MAUI) behaviors let you add functionality to user interface controls without having to subclass them. Instead, the functionality is implemented in a behavior class and attached to the control as if it was part of the control itself.

For further information on Behaviors please refer to the [.NET MAUI documentation](/dotnet/maui/fundamentals/behaviors).

## .NET MAUI Community Toolkit Behaviors

The .NET MAUI Community Toolkit provides a collection of pre-built, reusable behaviors to make developers lives easier. Here are the behaviors provided by the toolkit:

| Behavior | Description |
| --------- | ----------- |
| [`CharactersValidationBehavior`](characters-validation-behavior.md) | The `CharactersValidationBehavior` is a `Behavior` that allows the user to validate text input depending on specified parameters. |
| [`EmailValidationBehavior`](email-validation-behavior.md) | The `EmailValidationBehavior` is a `Behavior` that allows users to determine whether or not text input is a valid e-mail address. |
| [`MaskedBehavior`](masked-behavior.md) | The `MaskedBehavior` is a `Behavior` that allows the user to define an input mask for data entry. |
| [`MaxLengthReachedBehavior`](maximum-length-reached-behavior.md) | The `MaxLengthReachedBehavior` is a behavior that allows the user to trigger an action when a user has reached the maximum length allowed on an `InputView`. |
| [`UserStoppedTypingBehavior`](user-stopped-typing-behavior.md) | The `UserStoppedTypingBehavior` is a `Behavior` that will trigger an action when a user has stopped data input on controls for example `Entry`, `SearchBar` and `Editor`. Examples of its usage include triggering a search when a user has stopped entering their search query. |
