---
title: MVVM Toolkit info MVVMTK0051
author: Sergio0694
description: MVVM Toolkit info MVVMTK0051
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit info MVVMTK0051

This project producing one or more 'MVVMTK0045' warnings due to `[ObservableProperty]` being used on fields, which is not AOT compatible in WinRT scenarios, should set 'LangVersion' to 'preview' to enable partial properties and the associated code fixer (setting 'LangVersion=preview' is required to use `[ObservableProperty]` on partial properties and address these warnings).

The following sample generates MVVMTK0051:

```xml
<PropertyGroup>
    <LangVersion>10.0</LangVersion>
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

You can fix this by setting the language version to 'preview', like so:

```xml
<PropertyGroup>
    <LangVersion>preview</LangVersion>
</PropertyGroup>
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
