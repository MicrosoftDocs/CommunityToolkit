---
title: INotifyPropertyChanged attributes
author: Sergio0694
description: Attributes to inject MVVM support into partial classes
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, mvvm, componentmodel, property changed, notification, binding, net core, net standard
dev_langs:
  - csharp
---

# INotifyPropertyChanged attributes

The [`INotifyPropertyChanged`](/dotnet/api/communitytoolkit.mvvm.componentmodel.INotifyPropertyChangedAttribute) type is an attribute that allows inserting MVVM support code into existing types. Along with other related attributes ([`ObservableObject`](/dotnet/api/communitytoolkit.mvvm.componentmodel.ObservableObjectAttribute) and [`ObservableRecipient`](/dotnet/api/communitytoolkit.mvvm.componentmodel.ObservableRecipientdAttribute)), its purpose is to support developers in cases where the same functionality from these types was needed, but the target types were already implementing from another type. Since C# does not allow multiple inheritance, these attributes can instead be used to have the MVVM Toolkit generator add the same code right into those types, sidestepping this limitation.

> [!NOTE]
> In order to work, annotated types need to be in a [partial class](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods). If the type is nested, all types in the declaration syntax tree must also be annotated as partial. Not doing so will result in a compile errors, as the generator will not be able to generate a different partial declaration of that type with the requested additional code.

> [!NOTE]
> These attributes are only meant to be used in cases where the target types cannot just inherit from the equivalent types (eg. from `ObservableObject`). If that is possible, inheriting is the recommended approach, as it will reduce the binary size by avoiding creating duplicated code into the final assembly.

> **Platform APIs:** [`INotifyPropertyChanged`](/dotnet/api/communitytoolkit.mvvm.componentmodel.INotifyPropertyChangedAttribute), [`ObservableObject`](/dotnet/api/communitytoolkit.mvvm.componentmodel.ObservableObjectAttribute), [`ObservableRecipient`](/dotnet/api/communitytoolkit.mvvm.componentmodel.ObservableRecipientdAttribute)

## How to use them

Using any of these attributes is pretty straightforward: just add them to a [partial class](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods) and all the code from the corresponding types will automatically be generated into that type. For instance, consider this:

```csharp
[INotifyPropertyChanged]
public partial class MyViewModel : SomeOtherType
{    
}
```

This will generate a complete `INotifyPropertyChanged` implementation into the `MyViewModel` type, complete with additional helpers (such as `SetProperty`) that can be used to reduce verbosity. Here is a brief summary of the various attributes:
- [`INotifyPropertyChanged`](/dotnet/api/communitytoolkit.mvvm.componentmodel.INotifyPropertyChangedAttribute): implements the interface and adds helper methods to set properties and raise the events.
- [`ObservableObject`](/dotnet/api/communitytoolkit.mvvm.componentmodel.ObservableObjectAttribute): adds all the code from the `ObservableObject` type. It is conceptually equivalent to `INotifyPropertyChanged`, with the main difference being that it also implements `INotifyPropertyChanging`.
- [`ObservableRecipient`](/dotnet/api/communitytoolkit.mvvm.componentmodel.ObservableRecipientdAttribute): adds all the code from the `ObservableRecipient` type. In particular, this can be added to a type inheriting from `ObservableValidator` to combine the two.

## Examples

- Check out the [sample app](https://aka.ms/mvvmtoolkit/samples) (for multiple UI frameworks) to see the MVVM Toolkit in action.
- You can also find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.UnitTests).
