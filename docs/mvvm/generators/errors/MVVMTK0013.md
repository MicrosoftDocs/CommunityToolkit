---
title: MVVM Toolkit error MVVMTK0013
author: Sergio0694
description: MVVM Toolkit error MVVMTK0013
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0013

Cannot apply the `[RelayCommand]` attribute specifying to include a cancel command to methods not mapping to an asynchronous command type accepting a cancellation token.

The following sample generates MVVMTK0013:

```csharp
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel
{
    // The target method is synchronous, so no cancel command can be generated
    [RelayCommand(IncludeCancelCommand = true)]
    private void GreetUser(User user)
    {
    }
}
```

The same applies to an asynchronous method that does not take an input token:

```csharp
using System.Threading.Tasks;
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel
{
    // The target method is asynchronous but cannot be cancelled
    [RelayCommand(IncludeCancelCommand = true)]
    private async Task DoWorkAsync()
    {
    }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
