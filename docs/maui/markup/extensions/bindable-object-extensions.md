---
title: BindableObject extensions - .NET MAUI Community Toolkit
author: bijington
description: The BindableObject extensions provide a series of extension methods that support configuring Bindings on a BindableObject.
ms.date: 03/27/2022
---

# BindableObject extensions

The `BindableObject` extensions provide a series of extension methods that support configuring `Binding`s on a `BindableObject`.

The extensions offer the following methods:

## Bind

The `Bind` method offers a number of overloads providing different convenience around the setup of a `Binding`. For further information of the possibilities of `Binding` data in a .NET MAUI application refer to the [Microsoft documentation](/dotnet/maui/fundamentals/data-binding/).

### Example

```csharp
new Entry().Bind(Entry.TextProperty, nameof(ViewModel.RegistrationCode))
```

## BindCommand

## Assign

## Invoke