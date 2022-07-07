---
title: MVVM Toolkit error MVVMTK0009
author: Sergio0694
description: MVVM Toolkit error MVVMTK0009
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0009

The `CanExecute` name in `[RelayCommand]` must refer to a valid member in its parent type.

The following sample generates MVVMTK0009:

```csharp
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel
{
    private bool Foo => true;

    // There is no member named "Bar"
    [RelayCommand(CanExecute = "Bar")]
    private void GreetUser()
    {
    }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
