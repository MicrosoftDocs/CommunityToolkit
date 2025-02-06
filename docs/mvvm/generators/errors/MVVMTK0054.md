---
title: MVVM Toolkit error MVVMTK0054
author: Sergio0694
description: MVVM Toolkit error MVVMTK0054
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0054

A property using `[ObservableProperty]` returns a byref-like value (`[ObservableProperty]` must be used on properties of a non byref-like type).

The following sample generates MVVMTK0053:

```xml
<PropertyGroup>
    <LangVersion>preview</LangVersion>
</PropertyGroup>
```
```csharp
using System;
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    public partial ReadOnlySpan<char> Name { get; set; }
}
```

You cannot use `[ObservableObject]` on a property returning a ref struct type.

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
