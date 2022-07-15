---
title: MVVM Toolkit error MVVMTK0028
author: Sergio0694
description: MVVM Toolkit error MVVMTK0028
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0028

Types annotated with `[NotifyDataErrorInfo]` must inherit from `ObservableValidator`.

The following sample generates MVVMTK0028:

```csharp
using System.ComponentModel.DataAnnotations;
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

// This type is requesting validation support but doesn't have ObservableValidator features
[NotifyDataErrorInfo]
public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    [Required]
    private string name;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
