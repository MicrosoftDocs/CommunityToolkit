---
title: MVVM Toolkit error MVVMTK0031
author: Sergio0694
description: MVVM Toolkit error MVVMTK0031
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0031

Cannot apply the `[RelayCommand]` attribute specifying a task scheduler exception flow option to methods mapping to non-asynchronous command types.

The following sample generates MVVMTK0031:

```csharp
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel
{
    // Cannot use a custom exception flow option on a synchronous command method
    [RelayCommand(FlowExceptionsToTaskScheduler = false)]
    private void GreetUser(User user)
    {
    }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
