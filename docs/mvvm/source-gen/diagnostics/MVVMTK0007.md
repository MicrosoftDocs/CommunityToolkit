---
title: MVVM Toolkit error MVVMTK0007
author: Sergio0694
description: MVVM Toolkit error MVVMTK0007
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0007

Cannot apply `[RelayCommand]` to methods with a signature that doesn't match any of the existing relay command types.

The following sample generates MVVMTK0007:

```csharp
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel
{
    // This method returns a string value (synchronous commands have no return values)
    [RelayCommand]
    private string GreetUser() => ""Hello world!"";
}
```

And the same goes for methods with invalid parameters:

```csharp
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel
{
    // This method has two parameters, but synchronous commands can only take one.
    // Asynchronous commands can take two, if the second is a CancellationToken.
    [RelayCommand]
    private void GreetUser(object user, string name)
    {
        Console.WriteLine($"Hello {name}");
    }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
