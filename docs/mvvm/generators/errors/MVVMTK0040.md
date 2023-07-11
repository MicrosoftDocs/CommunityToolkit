---
title: MVVM Toolkit error MVVMTK0040
author: Sergio0694
description: MVVM Toolkit error MVVMTK0040
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0040

The backing fields of auto-properties cannot be annotated with `[ObservableProperty]` (the attribute can only be used directly on fields, and the generator will then handle generating the corresponding property). That is, using `[field: ObservableProperty]` from an auto-property declaration is not valid.

The following sample generates MVVMTK0040:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [field: ObservableProperty]
    public string? Name { get; set; }
}
```

You should instead make that property a field (eg. named `name`), and annotate that directly, like so:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    private string? name;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
