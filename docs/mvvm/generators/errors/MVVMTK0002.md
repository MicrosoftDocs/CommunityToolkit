---
title: MVVM Toolkit error MVVMTK0002
author: Sergio0694
description: MVVM Toolkit error MVVMTK0002
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0002

Cannot apply `[ObservableObject]` to a type that already declares the `INotifyPropertyChanged` interface.

The following sample generates MVVMTK0002:

```csharp
using System.ComponentModel;
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

// The type already declares the interface
[ObservableObject]
public partial class SampleViewModel : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler? PropertyChanged;
}
```

And the same goes for inherited interface implementations:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

// The type inherits from ObservableObject, which implements INotifyPropertyChanged
[ObservableObject]
public partial class SampleViewModel : ObservableObject
{
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
