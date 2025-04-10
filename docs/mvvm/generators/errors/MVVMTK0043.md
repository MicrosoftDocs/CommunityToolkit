---
title: MVVM Toolkit error MVVMTK0043
author: Sergio0694
description: MVVM Toolkit error MVVMTK0043
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0043

Properties annotated with `[ObservableProperty]` must be partial properties with a getter and a setter that is not init-only.

The following sample generates MVVMTK0043:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    public partial string? Name { get; }
}
```

You should ensure that properties have both a `get` and a `set` accessor, like so:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    public partial string? Name { get; set; }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
