---
title: MVVM Toolkit error MVVMTK0036
author: Sergio0694
description: MVVM Toolkit error MVVMTK0036
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0036

All attributes targeting the generated field or property for a method annotated with `[RelayCommand]` must correctly be resolved to valid types. This error is shown when a given `field:` or `property:` attribute over a method with `[RelayCommand]` is not correctly resolved to a type, which helps identifying issues at compile time as soon as possible. A common example where this can happen is if a `using` directive for the attribute is missing.

The following sample generates MVVMTK0036:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    private int counter;

    [RelayCommand]
    [property: JsonIgnore]
    private void IncrementCounter()
    {
        Counter++;
    }
}
```

You can see that `JsonIgnore` has no `using` directive here, and as such is not resolved correctly. You can fix this by updating the code as follows:

```csharp
using System.Text.Json.Serialization;
using CommunityToolkit.Mvvm.ComponentModel;
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    private int counter;

    [RelayCommand]
    [property: JsonIgnore]
    private void IncrementCounter()
    {
        Counter++;
    }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
