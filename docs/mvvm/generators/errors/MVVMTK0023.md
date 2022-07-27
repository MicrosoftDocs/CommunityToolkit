---
title: MVVM Toolkit error MVVMTK0023
author: Sergio0694
description: MVVM Toolkit error MVVMTK0023
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0023

Methods with multiple overloads cannot be annotated with `[RelayCommand]`, as command methods must be unique within their containing type.

The following sample generates MVVMTK0023:

```csharp
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel
{
    [RelayCommand]
    private void GreetUser()
    {
    }

    // Cannot have an overload of a command method
    [RelayCommand]
    private void GreetUser(object value)
    {
    }
}
```

The same applies when overloads are present in base types as well:

```csharp
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class BaseViewModel
{
    [RelayCommand]
    private void GreetUser()
    {
    }
}

public partial class SampleViewModel : BaseViewModel
{
    // The base type already has an overload of this command method
    [RelayCommand]
    private void GreetUser(object value)
    {
    }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
