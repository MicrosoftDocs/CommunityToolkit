---
title: MVVM Toolkit warning MVVMTK0047
author: Sergio0694
description: MVVM Toolkit warning MVVMTK0047
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit warning MVVMTK0047

Using `[GeneratedBindableCustomProperty]` on types that also use `[ObservableProperty]` on any declared (or inherited) fields is not supported, and partial properties should be used instead (the `[GeneratedBindableCustomProperty]` generator cannot see the generated property that is produced by the MVVM Toolkit generator).

The following sample generates MVVMTK0047:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[GeneratedBindableCustomProperty]
public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    private string? name;
}
```

You should instead make that field a partial property (eg. named `Name`), like so:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[GeneratedBindableCustomProperty]
public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    public partial string? Name { get; set; }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
