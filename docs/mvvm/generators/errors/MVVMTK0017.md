---
title: MVVM Toolkit error MVVMTK0017
author: Sergio0694
description: MVVM Toolkit error MVVMTK0017
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0017

Cannot apply `[INotifyPropertyChanged]` to a type that already has this attribute or `[ObservableObject]` applied to it (including base types).

The following sample generates MVVMTK0017:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[INotifyPropertyChanged]
public partial class A
{
}

// The base type already has [INotifyPropertyChanged]
[INotifyPropertyChanged]
public partial class B : A
{
}
```

The same applies when multiple attributes are used as well:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

// Cannot use both [INotifyPropertyChanged] and [ObservableObject]
[INotifyPropertyChanged]
[ObservableObject]
public partial class A
{
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
