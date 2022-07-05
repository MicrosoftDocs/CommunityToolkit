---
title: MVVM Toolkit error MVVMTK0011
author: Sergio0694
description: MVVM Toolkit error MVVMTK0011
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0011

The `CanExecute` name in `[RelayCommand]` must refer to a compatible member (either a property or a method) to be used in a generated command.

The following sample generates MVVMTK0011:

```csharp
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel
{
    private bool Foo { set { } }

    // The target property "Foo" does not have a getter
    [RelayCommand(CanExecute = nameof(Foo))]
    private void GreetUser()
    {
    }
}
```

The same goes for a target member with an invalid type:

```csharp
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel
{
    // The property returns a string, not a bool
    private string Foo => ""Hi!"";

    [RelayCommand(CanExecute = nameof(Foo))]
    private void GreetUser()
    {
    }
}
```

The same rules apply to both properties and methods.

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
