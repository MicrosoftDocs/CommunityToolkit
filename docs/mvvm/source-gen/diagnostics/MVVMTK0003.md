---
title: MVVM Toolkit error MVVMTK0003
author: Sergio0694
description: MVVM Toolkit error MVVMTK0003
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0003

Cannot apply `[ObservableObject]` to a type that already declares the `INotifyPropertyChanging` interface.

The following sample generates MVVMTK0003:

```csharp
using System.ComponentModel;
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

// The type already declares the interface
[ObservableObject]
public partial class SampleViewModel : INotifyPropertyChanging
{
    public event PropertyChangingEventHandler? PropertyChanging;
}
```

And the same goes for inherited interface implementations:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

// The type inherits from ObservableObject, which implements INotifyPropertyChanging
[ObservableObject]
public partial class SampleViewModel : ObservableObject
{
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
