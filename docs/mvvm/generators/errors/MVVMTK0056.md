---
title: MVVM Toolkit info MVVMTK0056
author: Sergio0694
description: MVVM Toolkit info MVVMTK0056
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit info MVVMTK0056

Semi-auto properties should be converted to partial properties using `[ObservableProperty]` when possible, which is recommended (doing so makes the code less verbose and results in more optimized code).

The following sample generates MVVMTK0056:

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
    public string? Name
    {
        get;
        set => SetProperty(ref field, value);
    }
}
```

You can fix this by converting the property to use `[ObservableProperty]` instead:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    public partial string? Name { get; set; }
}
```

There is also a built-in code fixer for this diagnostic, to easily fix all occurrences in a single click.

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
