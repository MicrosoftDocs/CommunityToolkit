---
title: MVVM Toolkit error MVVMTK0041
author: Sergio0694
description: MVVM Toolkit error MVVMTK0041
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0041

The C# language version must be set to 'preview' when using `[ObservableProperty]` on partial properties for the source generators to emit valid code.

This is required because the generated code for `[ObservableProperty]` on partial properties uses some preview features. Make sure to add `<LangVersion>preview</LangVersion>` (or above) to your .csproj file.

To learn more about how to enable a newer C# version on older frameworks, [see this blog post](https://sergiopedri.medium.com/enabling-and-using-c-9-features-on-older-and-unsupported-runtimes-ce384d8debb).

The following sample generates MVVMTK0041:

```xml
<PropertyGroup>
    <LangVersion>13.0</LangVersion>
</PropertyGroup>
```
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
