---
title: MVVM Toolkit error MVVMTK0010
author: Sergio0694
description: MVVM Toolkit error MVVMTK0010
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0010

Cannot set the `CanExecute` name in `[RelayCommand]` to one that has multiple matches in its parent type (it must refer to a single compatible member).

The following sample generates MVVMTK0010:

```csharp
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel
{
    private bool Foo => true;

    private bool Foo() => true;

    // There are two members named "Foo", so the match is ambiguous
    [RelayCommand(CanExecute = nameof(Foo))]
    private void GreetUser()
    {
    }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
