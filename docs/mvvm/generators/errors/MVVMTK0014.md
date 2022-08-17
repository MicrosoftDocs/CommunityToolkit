---
title: MVVM Toolkit error MVVMTK0014
author: Sergio0694
description: MVVM Toolkit error MVVMTK0014
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0014

The name of fields annotated with `[ObservableProperty]` should use "lowerCamel", "_lowerCamel" or "m_lowerCamel" pattern to avoid collisions with the generated properties.

The following sample generates MVVMTK0014:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    // The target field would generate a property with the same name
    [ObservableProperty]
    private string Name;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
