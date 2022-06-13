---
title: MVVM Toolkit error MVVMTK0019
author: Sergio0694
description: MVVM Toolkit error MVVMTK0019
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0019

Fields annotated with `[ObservableProperty]` must be contained in a type that inherits from `ObservableObject` or that is annotated with `[ObservableObject]` or `[INotifyPropertyChanged]` (including base types).

The following sample generates MVVMTK0019:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class MyViewModel : INotifyPropertyChanged
{
    // The containing type does not have the ObservableObject functionality.
    // The [ObservableProperty] attribute requires additional helper methods to work.
    [ObservableProperty]
    public int number;

    public event PropertyChangedEventHandler PropertyChanged;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
