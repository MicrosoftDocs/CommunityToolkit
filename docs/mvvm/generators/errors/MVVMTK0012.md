---
title: MVVM Toolkit error MVVMTK0012
author: Sergio0694
description: MVVM Toolkit error MVVMTK0012
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0012

Cannot apply the `[RelayCommand]` attribute specifying a concurrency control option to methods mapping to non-asynchronous command types.

The following sample generates MVVMTK0012:

```csharp
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel
{
    // The target method is synchronous, so the option is not valid
    [RelayCommand(AllowConcurrentExecutions = false)]
    private void GreetUser(User user)
    {
    }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
