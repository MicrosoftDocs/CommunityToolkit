---
title: MVVM source generators
author: Sergio0694
description: An overview of Roslyn source generators to power MVVM scenarios
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, mvvm, componentmodel, property changed, notification, binding, net core, net standard
dev_langs:
  - csharp
---

# MVVM source generators

Starting with version 8.0, the MVVM Toolkit includes brand new Roslyn source generators that will help greatly reduce boilerplate when writing code using the MVVM architecture. They can simplify scenarios where you need to setup observable properties, commands and more. If you're not familiar with source generators, you can read more about them [here](/dotnet/csharp/roslyn-sdk/source-generators-overview). This is a simplified view of how they work:

:::image type="content" source="/dotnet/csharp/roslyn-sdk/media/source-generators/source-generator-visualization.png#lightbox" alt-text="Graphic describing the different parts of source generation":::

This means that as you're writing code, the MVVM Toolkit generator will now take care of generating additional code for you behind the scenes, so you don't have to worry about it. This code will then be compiled and included in your application, so the end result is exactly the same as if you had written all that extra code manually, but without having to do all of that extra work! 🎉

For instance, wouldn't it be great if instead of having to setup an observable property normally:

```csharp
private string? name;

public string? Name
{
    get => name;
    set => SetProperty(ref name, value);
}
```

You could just have a simple annotated field to express the same?

```csharp
[ObservableProperty]
private string? name;
```

What about creating a command:

```csharp
private void SayHello()
{
    Console.WriteLine("Hello");
}

private ICommand? sayHelloCommand;

public ICommand SayHelloCommand => sayHelloCommand ??= new RelayCommand(SayHello);
```

What if we could just have our method, and nothing else?

```csharp
[RelayCommand]
private void SayHello()
{
    Console.WriteLine("Hello");
}
```

With the new MVVM source generators, all of this is possible, and much more! 🙌

These docs will go over exactly what features are included with the MVVM generators and how to use them.

## Examples

- Check out the [sample app](https://aka.ms/mvvmtoolkit/samples) (for multiple UI frameworks) to see the MVVM Toolkit in action.
- You can also find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.UnitTests).
