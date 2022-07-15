---
title: MVVM Toolkit error MVVMTK0018
author: Sergio0694
description: MVVM Toolkit error MVVMTK0018
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0018

Cannot apply `[ObservableObject]` to a type that already has this attribute or `[INotifyPropertyChanged]` applied to it (including base types).

The following sample generates MVVMTK0018:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[INotifyPropertyChanged]
public partial class A
{
}

// The base type is already using [INotifyPropertyChanged]
[ObservableObject]
public partial class B : A
{
}
```

The same applies when multiple attributes are used on the same type:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

// Cannot use both [ObservableObject] and [INotifyPropertyChanged]
[INotifyPropertyChanged]
[ObservableObject]
public partial class A
{
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
