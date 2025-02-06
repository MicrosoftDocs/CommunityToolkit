---
title: MVVM Toolkit error MVVMTK0055
author: Sergio0694
description: MVVM Toolkit error MVVMTK0055
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0055

A property using `[ObservableProperty]` returns a pointer-like value (`[ObservableProperty]` must be used on properties of a non pointer-like type).

The following sample generates MVVMTK0055:

```xml
<PropertyGroup>
    <LangVersion>preview</LangVersion>
</PropertyGroup>
```
```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public unsafe partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    public partial char* Name { get; set; }
}
```

You cannot use `[ObservableObject]` on a property returning a pointer type.

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
