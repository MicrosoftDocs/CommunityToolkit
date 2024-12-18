---
title: MVVM Toolkit error MVVMTK0053
author: Sergio0694
description: MVVM Toolkit error MVVMTK0053
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0053

A property using `[ObservableProperty]` returns a value by reference (`[ObservableProperty]` must be used on properties returning a type by value).

The following sample generates MVVMTK0053:

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
    public partial ref string? Name { get; set; }
}
```

You cannot use `[ObservableObject]` on a property returning a `ref` or a `ref readonly` value.

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
