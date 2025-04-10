---
title: MVVM Toolkit info MVVMTK0042
author: Sergio0694
description: MVVM Toolkit info MVVMTK0042
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit info MVVMTK0042

Fields using `[ObservableProperty]` can be converted to partial properties instead, which is recommended (doing so improves the developer experience and allows other generators and analyzers to correctly see the generated property as well).

The following sample generates MVVMTK0042:

```xml
<PropertyGroup>
    <LangVersion>preview</LangVersion>
</PropertyGroup>
```
```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

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

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    public partial string? Name { get; set; }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
