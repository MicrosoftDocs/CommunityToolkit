---
title: ObservableProperty attribute
author: Sergio0694
description: An attribute to generate observable properties
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, mvvm, componentmodel, property changed, notification, binding, net core, net standard
dev_langs:
  - csharp
---

# ObservableProperty attribute

The [`ObservableProperty`](/dotnet/api/communitytoolkit.mvvm.componentmodel.ObservablePropertyAttribute) type is an attribute that allows generating observable properties from annotated fields. Its purpose is to greatly reduce the amount of boilerplate that is needed to define observable properties.

> [!NOTE]
> In order to work, annotated fields need to be in a [partial class](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods) with the necessary `INotifyPropertyChanged` infrastructure. If the type is nested, all types in the declaration syntax tree must also be annotated as partial. Not doing so will result in a compile errors, as the generator will not be able to generate a different partial declaration of that type with the requested observable property.

> **Platform APIs:** [`ObservableProperty`](/dotnet/api/communitytoolkit.mvvm.componentmodel.ObservablePropertyAttribute), [`NotifyPropertyChangedFor`](/dotnet/api/communitytoolkit.mvvm.componentmodel.NotifyPropertyChangedForAttribute), [`NotifyCanExecuteChangedFor`](/dotnet/api/communitytoolkit.mvvm.componentmodel.NotifyCanExecuteChangedForAttribute), [`NotifyDataErrorInfo`](/dotnet/api/communitytoolkit.mvvm.componentmodel.NotifyDataErrorInfoAttribute), [`NotifyPropertyChangedRecipients`](/dotnet/api/communitytoolkit.mvvm.componentmodel.NotifyPropertyChangedRecipientsAttribute), [`ICommand`](/dotnet/api/system.windows.input.icommand), [`IRelayCommand`](/dotnet/api/communitytoolkit.mvvm.input.IRelayCommand), [ObservableValidator](/dotnet/api/microsoft.toolkit.mvvm.componentmodel.ObservableValidator), [`PropertyChangedMessage<T>`](/dotnet/api/communitytoolkit.mvvm.Messaging.Messages.PropertyChangedMessage-1), [`IMessenger`](/dotnet/api/communitytoolkit.mvvm.Messaging.IMessenger)

## How it works

The `ObservableProperty` attribute can be used to annotate a field in a partial type, like so:

```csharp
[ObservableProperty]
private string? name;
```

And it will generate an observable property like this:

```csharp
public string? Name
{
    get => name;
    set => SetProperty(ref name, value);
}
```

It will also do so with an optimized implementation, so the end result will be even faster.

> [!NOTE]
> The name of the generated property will be created based on the field name. The generator assumes the field is named either `lowerCamel`, `_lowerCamel` or `m_lowerCamel`, and it will transform that to be `UpperCamel` to follow proper .NET naming conventions. The resulting property will always have public accessors, but the field can be declared with any visibility (`private` is recommended).

## Running code upon changes

The generated code is actually a bit more complex than this, and the reason for that is that it also exposes some methods you can implement to hook into the notification logic, and run additional logic when the property is about to be updated and right after it is updated, if needed. That is, the generated code is actually similar to this:

```csharp
public string? Name
{
    get => name;
    set
    {
        if (!EqualityComparer<string?>.Default.Equals(name, value))
        {
            OnNameChanging(value);
            OnPropertyChanging();
            name = value;
            OnNameChanged(value);
            OnPropertyChanged();
        }
    }
}

partial void OnNameChanging(string? value);
partial void OnNameChanged(string? value);
```

This allows you to implement any of those two methods to inject additional code:

```csharp
[ObservableProperty]
private string? name;

partial void OnNameChanging(string? value)
{
    Console.WriteLine($"Name is about to change to {value}");
}

partial void OnNameChanged(string? value)
{
    Console.WriteLine($"Name has changed to {value}");
}
```

You're free to only implement one of these two methods, or neither. If they are not implemented (or if only one is), the entire call(s) will just be removed by the compiler, so there will be no performance hit at all for cases where this additional functionality is not required.

> [!NOTE]
> The generated methods are [partial methods](/dotnet/csharp/language-reference/keywords/partial-method) with no implementation, meaning that if you choose to implement them, you cannot specify an explicit accessibility for them. That is, implementations of these methods should also be declared as just `partial` methods, and they will always implicitly have private accessibility. Trying to add an explicit accessibility (eg. adding `public` or `private`) will result in an error, as that is not allowed in C#.

## Notifying dependent properties

Imagine you had a `FullName` property you wanted to raise a notification for whenever `Name` changes. You can do that by using the `NotifyPropertyChangedFor` attribute, like so:

```csharp
[ObservableProperty]
[NotifyPropertyChangedFor(nameof(FullName))]
private string? name;
```

This will result in a generated property equivalent to this:

```csharp
public string? Name
{
    get => name;
    set
    {
        if (SetProperty(ref name, value))
        {
            OnPropertyChanged("FullName");
        }
    }
}
```

## Notifying dependent commands

Imagine you had a command whose execution state was dependent on the value of this property. That is, whenever the property changed, the execution state of the command should be invalidated and computed again. In other words, [`ICommand.CanExecuteChanged`](/dotnet/api/system.windows.input.icommand.canexecutechanged) should be raised again. You can achieve this by using the `NotifyCanExecuteChangedFor` attribute:

```csharp
[ObservableProperty]
[NotifyCanExecuteChangedFor(nameof(MyCommand))]
private string? name;
```

This will result in a generated property equivalent to this:

```csharp
public string? Name
{
    get => name;
    set
    {
        if (SetProperty(ref name, value))
        {
            MyCommand.NotifyCanExecuteChanged();
        }
    }
}
```

In order for this to work, the target command has to be some [`IRelayCommand`](/dotnet/api/microsoft.toolkit.mvvm.input.IRelayCommand) property.

## Requesting property validation

If the property is declared in a type that inherits from [ObservableValidator](/dotnet/api/microsoft.toolkit.mvvm.componentmodel.ObservableValidator), it is also possible to annotate it with any validation attributes and then request the generated setter to trigger validation for that property. This can be achieved with the `NotifyDataErrorInfo` attribute:

```csharp
[ObservableProperty]
[NotifyDataErrorInfo]
[Required]
[MinLength(2)] // Any other validation attributes too...
private string? name;
```

This will result in the following property being generated:

```csharp
public string? Name
{
    get => name;
    set
    {
        if (SetProperty(ref name, value))
        {
            ValidateProperty(value, "Value2");
        }
    }
}
```

That generated `ValidateProperty` call will then validate the property and update the state of the `ObservableValidator` object, so that UI components can react to it and display any validation errors appropriately.

> [!NOTE]
> By design, only field attributes that inherit from [`ValidationAttribute`](/dotnet/api/system.componentmodel.dataannotations.validationattribute) will be forwarded to the generated property. This is done specifically to support data validation scenarios. All other field attributes will be ignored, so it is not currently possible to add additional custom attributes on a field and have them also be applied to the generated property. If that is required (eg. to control serialization), consider using a traditional manual property instead.

## Sending notification messages

If the property is declared in a type that inherits from [`ObservableRecipient`](/dotnet/api/microsoft.toolkit.mvvm.componentmodel.ObservableRecipient), you can use the `NotifyPropertyChangedRecipients` attribute to instruct the generator to also insert code to send a property changed message for the property change. This will allow registered recipients to dynamically react to the change. That is, consider this code:

```csharp
[ObservableProperty]
[NotifyPropertyChangedRecipients]
private string? name;
```

This will result in the following property being generated:

```csharp
public string? Name
{
    get => name;
    set
    {
        string? oldValue = name;

        if (SetProperty(ref name, value))
        {
            Broadcast(oldValue, value);
        }
    }
}
```

That generated `Broadcast` call will then send a new [`PropertyChangedMessage<T>`](/dotnet/api/communitytoolkit.mvvm.Messaging.Messages.PropertyChangedMessage-1) using the `IMessenger` instance in use in the current viewmodel, to all registered subscribers.

## Examples

- Check out the [sample app](https://aka.ms/mvvmtoolkit/samples) (for multiple UI frameworks) to see the MVVM Toolkit in action.
- You can also find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.UnitTests).
