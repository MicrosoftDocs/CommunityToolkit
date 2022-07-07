---
title: MVVM Toolkit error MVVMTK0016
author: Sergio0694
description: MVVM Toolkit error MVVMTK0016
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0016

The target(s) of `[NotifyCanExecuteChangedFor]` must be an accessible `IRelayCommand` property in its parent type.

The following sample generates MVVMTK0016:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    // The containing type has no command named "FooBar"
    [ObservableProperty]
    [NotifyCanExecuteChangedFor("FooBar")]
    private string name;
}
```

The same applies if the target method is not a command:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    // The target member "Foo" is a method, not a command
    [ObservableProperty]
    [NotifyCanExecuteChangedFor(nameof(Foo))]
    private string name;

    public void Foo()
    {
    }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
