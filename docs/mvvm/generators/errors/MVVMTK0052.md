---
title: MVVM Toolkit error MVVMTK0052
author: Sergio0694
description: MVVM Toolkit error MVVMTK0052
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0052

A property using `[ObservableProperty]` is not an incomplete partial definition part (`[ObservableProperty]` must be used on partial property definitions with no implementation part).

The following sample generates MVVMTK0052:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    public partial string? Name { get; set; }

    public partial string? Name
    {
        get;
        set => field = value;
    }
}
```

You should remove the partial implementation, and only use `[ObservableProperty]` on the partial declaration part.

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
