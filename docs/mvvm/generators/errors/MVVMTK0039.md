---
title: MVVM Toolkit warning MVVMTK0039
author: Sergio0694
description: MVVM Toolkit warning MVVMTK0036
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit warning MVVMTK0039

Asynchronous methods annotated with `[RelayCommand]` should return a `Task` value, and not be `async void`. This allows the generator to generate asynchronous commands instead (ie. `AsyncRelayCommand` or `AsyncRelayCommand<T>`), which offer additional features such as concurrency control, tracking execution, and more.

The following sample generates MVVMTK0039:

```csharp
using System.Threading.Tasks;
using CommunityToolkit.Mvvm.ComponentModel;
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [RelayCommand]
    private async void DoWorkAsync()
    {
        await Task.Delay(1000); // Do some work
    }
}
```

You can see that `DoWorkAsync` is asynchronous, but is just returning `void`. You can fix this by updating the code as follows:

```csharp
using System.Threading.Tasks;
using CommunityToolkit.Mvvm.ComponentModel;
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [RelayCommand]
    private async Task DoWorkAsync()
    {
        await Task.Delay(1000);
    }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
