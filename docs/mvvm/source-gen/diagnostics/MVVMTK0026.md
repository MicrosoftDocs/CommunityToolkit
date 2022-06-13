---
title: MVVM Toolkit error MVVMTK0026
author: Sergio0694
description: MVVM Toolkit error MVVMTK0026
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0026

Cannot apply `[NotifyDataErrorInfo]` to fields that don't have any validation attributes to use during validation.

The following sample generates MVVMTK0026:

```csharp
using System.ComponentModel.DataAnnotations;
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableValidator
{
    // This property is requesting validation but has no validation attributes
    [ObservableProperty]
    [NotifyDataErrorInfo]
    private string name;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
