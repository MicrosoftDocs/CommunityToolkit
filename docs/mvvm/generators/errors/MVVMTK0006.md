---
title: MVVM Toolkit error MVVMTK0006
author: Sergio0694
description: MVVM Toolkit error MVVMTK0006
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0006

Cannot apply `[ObservableProperty]` to fields with validation attributes if they are declared in a type that doesn't inherit from `ObservableValidator`.

The following sample generates MVVMTK0006:

```csharp
using System.ComponentModel.DataAnnotations;
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[INotifyPropertyChanged]
public partial class SampleViewModel
{
    // The field has a validation attribute (the [Required] attribute), but the
    // containing type (SampleViewModel) doesn't inherit from ObservableValidator
    [ObservableProperty]
    [Required]
    private string name;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
