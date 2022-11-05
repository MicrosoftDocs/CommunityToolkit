---
title: RelayCommand attribute
author: Sergio0694
description: An attribute to generate relay command properties
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, mvvm, componentmodel, property changed, notification, binding, net core, net standard
dev_langs:
  - csharp
---

# RelayCommand attribute

The [`RelayCommand`](/dotnet/api/communitytoolkit.mvvm.input.RelayCommandAttribute) type is an attribute that allows generating relay command properties for annotated methods. Its purpose is to completely eliminate the boilerplate that is needed to define commands wrapping private methods in a viewmodel.

> [!NOTE]
> In order to work, annotated methods need to be in a [partial class](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods). If the type is nested, all types in the declaration syntax tree must also be annotated as partial. Not doing so will result in a compile errors, as the generator will not be able to generate a different partial declaration of that type with the requested command.

> **Platform APIs:** [`RelayCommand`](/dotnet/api/communitytoolkit.mvvm.input.RelayCommandAttribute), [`ICommand`](/dotnet/api/system.windows.input.icommand), [`IRelayCommand`](/dotnet/api/communitytoolkit.mvvm.input.IRelayCommand), [`IRelayCommand<T>`](/dotnet/api/communitytoolkit.mvvm.input.IRelayCommand-1), [`IAsyncRelayCommand`](/dotnet/api/communitytoolkit.mvvm.input.IAsyncRelayCommand), [`IAsyncRelayCommand<T>`](/dotnet/api/communitytoolkit.mvvm.input.IAsyncRelayCommand-1), [`Task`](/dotnet/api/system.threading.tasks.task), [`CancellationToken`](/dotnet/api/system.threading.cancellationtoken)

## How it works

The `RelayCommand` attribute can be used to annotate a method in a partial type, like so:

```csharp
[RelayCommand]
private void GreetUser()
{
    Console.WriteLine("Hello!");
}
```

And it will generate a command like this:

```csharp
private RelayCommand? greetUserCommand;

public IRelayCommand GreetUserCommand => greetUserCommand ??= new RelayCommand(GreetUser);
```

> [!NOTE]
> The name of the generated command will be created based on the method name. The generator will use the method name and append "Command" at the end, and it will strip the "On" prefix, if present. Additionally, for asynchronous methods, the "Async" suffix is also stripped before "Command" is appeneded.

## Command parameters

The `[RelayCommand]` attribute supports creating commands for methods with a parameter. In that case, it will automatically change the generated command to be an [`IRelayCommand<T>`](/dotnet/api/communitytoolkit.mvvm.input.IRelayCommand-1) instead, accepting a parameter of the same type:

```csharp
[RelayCommand]
private void GreetUser(User user)
{
    Console.WriteLine($"Hello {user.Name}!");
}
```

This will result in the following generated code:

```csharp
private RelayCommand<User>? greetUserCommand;

public IRelayCommand<User> GreetUserCommand => greetUserCommand ??= new RelayCommand<User>(GreetUser);
```

The resulting command will automatically use the type of the argument as its type argument.

## Asynchronous commands

The `[RelayCommand]` command also supports wrapping asynchronous methods, via the [`IAsyncRelayCommand`](/dotnet/api/communitytoolkit.mvvm.input.IAsyncRelayCommand) and [`IAsyncRelayCommand<T>`](/dotnet/api/communitytoolkit.mvvm.input.IAsyncRelayCommand-1) interfaces. This is handled automatically whenever a method returns a [`Task`](/dotnet/api/system.threading.tasks.task) type. For instance:

```csharp
[RelayCommand]
private async Task GreetUserAsync()
{
    User user = await userService.GetCurrentUserAsync();

    Console.WriteLine($"Hello {user.Name}!");
}
```

This will result in the following code:

```csharp
private AsyncRelayCommand? greetUserCommand;

public IAsyncRelayCommand GreetUserCommand => greetUserCommand ??= new AsyncRelayCommand(GreetUserAsync);
```

If the method takes a parameter, the resulting command will also be generic.

There is a special case when the method has a [`CancellationToken`](/dotnet/api/system.threading.cancellationtoken), as that will be propagated to the command to enable cancellation. That is, a method like this:

```csharp
[RelayCommand]
private async Task GreetUserAsync(CancellationToken token)
{
    try
    {
        User user = await userService.GetCurrentUserAsync(token);

        Console.WriteLine($"Hello {user.Name}!");
    }
    catch (OperationCanceledException)
    {
    }
}
```

Will result in the generated command passing a token to the wrapped method. This allows consumers to just call [`IAsyncRelayCommand.Cancel`](/dotnet/api/communitytoolkit.mvvm.input.iasyncrelaycommand.cancel) to signal that token, and to allow pending operations to be stopped correctly.

## Enabling and disabling commands

It is often useful to be able to disable commands, and to then later on invalidate their state and have them check again whether they can be executed or not. In order to support this, the `RelayCommand` attribute exposes the `CanExecute` property, which can be used to indicate a target property or method to use to evaluate whether a command can be executed:

```csharp
[RelayCommand(CanExecute = nameof(CanGreetUser))]
private void GreetUser(User? user)
{
    Console.WriteLine($"Hello {user!.Name}!");
}

private bool CanGreetUser(User? user)
{
    return user is not null;
}
```

This way, `CanGreetUser` is invoked when the button is first bound to the UI (eg. to a button), and then it is invoked again every time [`IRelayCommand.NotifyCanExecuteChanged`](/dotnet/api/communitytoolkit.mvvm.input.irelaycommand.notifycanexecutechanged) is invoked on the command.

For instance, this is how a command can be bound to a property to control its state:

```csharp
[ObservableProperty]
[NotifyCanExecuteChangedFor(nameof(GreetUserCommand))]
private User? selectedUser;
```
```xml
<!-- Note: this example uses traditional XAML binding syntax -->
<Button
    Content="Greet user"
    Command="{Binding GreetUserCommand}"
    CommandParameter="{Binding SelectedUser}"/>
```

In this example, the generated `SelectedUser` property will invoke `GreetUserCommand.NotifyCanExecuteChanged()` method every time its value changes. The UI has a `Button` control binding to `GreetUserCommand`, meaning every time its `CanExecuteChanged` event is raised, it will call its `CanExecute` method again. This will cause the wrapped `CanGreetUser` method to be evaluated, which will return the new state for the button based on whether or not the input `User` instance (which in the UI is bound to the `SelectedUser` property) is `null` or not. This means that whenever `SelectedUser` is changed, `GreetUserCommand` will become enabled or not based on whether that property has a value, which is the desired behavior in this scenario.

> [!NOTE]
> The command will **not** automatically be aware of when the return value for the `CanExecute` method or property has changed. It is up to the developer to call `IRelayCommand.NotifyCanExecuteChanged` to invalidate the command and request the linked `CanExecute` method to be evaluated again to then update the visual state of the control bound to the command.

## Handling concurrent executions

Whenever a command is asynchronous, it can be configured to decide whether to allow concurrent executions or not. When using the `RelayCommand` attribute, this can be set via the `AllowConcurrentExecutions` property. The default is `false`, meaning that until an execution is pending, the command will signal its state as being disabled. If it instead is set to `true`, any number of concurrent invocations can be queued.

Note that if a command accepts a cancellation token, a token will also be canceled if a concurrent execution is requested. The main difference is that if concurrent executions are allowed, the command will remain enabled and it will start a new requested execution without waiting for the previous one to actually complete.

## Handling asynchronous exceptions

There are two different ways async relay commands handle exceptions:
- **Await and rethrow (default)**: when the command awaits the completion of an invocation, any exceptions will naturally be thrown on the same synchronization context. That usually means that exceptions being thrown would just crash the app, which is a behavior consistent with that of synchronous commands (where exceptions being thrown will also crash the app).
- **Flow exceptions to task scheduler**: if a command is configured to flow exceptions to the task scheduler, exceptions being thrown will not crash the app, but instead they will both become available through the exposed [`IAsyncRelayCommand.ExecutionTask`](/dotnet/api/communitytoolkit.mvvm.input.iasyncrelaycommand.executiontask) as well as bubbling up to the [`TaskScheduler.UnobservedTaskException`](/dotnet/api/system.threading.tasks.taskscheduler.unobservedtaskexception). This enables more advanced scenarios (such as having UI components bind to the task and display different results based on the outcome of the operation), but it is more complex to use correctly.

The default behavior is having commands await and rethrow exceptions. This can be configured via the `FlowExceptionsToTaskScheduler` property:

```csharp
[RelayCommand(FlowExceptionsToTaskScheduler = true)]
private async Task GreetUserAsync(CancellationToken token)
{
    User user = await userService.GetCurrentUserAsync(token);

    Console.WriteLine($"Hello {user.Name}!");
}
```

In this case, the `try/catch` is not needed, as exceptions will not crash the app anymore. Note that this will also cause other unrelated exceptions to not be rethrown automatically, so you should carefully decide how to approach each individual scenario and configure the rest of the code appropriately.

## Cancel commands for asynchronous operations

One last option for asynchronous commands is the ability to request a cancel command to be generated. This is an `ICommand` wrapping an async relay command that can be used to request the cancellation of an operation. This command will automatically signal its state to reflect whether or not it can be used at any given time. For instance, if the linked command is not executing, it will report its state as also not being executable. This can be used as follows:

```csharp
[RelayCommand(IncludeCancelCommand = true)]
private async Task DoWorkAsync(CancellationToken token)
{
    // Do some long running work...
}
```

This will cause a `DoWorkCancelCommand` property to also be generated. This can then be bound to some other UI component to easily let users cancel pending asynchronous operations.

## Examples

- Check out the [sample app](https://aka.ms/mvvmtoolkit/samples) (for multiple UI frameworks) to see the MVVM Toolkit in action.
- You can also find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.UnitTests).
