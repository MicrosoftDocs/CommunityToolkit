---
title: MVVM Toolkit error MVVMTK0025
author: Sergio0694
description: MVVM Toolkit error MVVMTK0025
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0025

Cannot apply `[NotifyDataErrorInfo]` to fields that are declared in a type that doesn't inherit from `ObservableValidator`.

The following sample generates MVVMTK0025:

```csharp
using System.ComponentModel.DataAnnotations;
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[INotifyPropertyChanged]
public partial class SampleViewModel
{
    // This field is using validation features but its containing type does not
    // inherit from ObservableValidator. As such, validation is not supported.
    [ObservableProperty]
    [Required]
    [NotifyDataErrorInfo]
    private string name;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
