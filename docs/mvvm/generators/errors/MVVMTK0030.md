---
title: MVVM Toolkit warning MVVMTK0030
author: Sergio0694
description: MVVM Toolkit warning MVVMTK0030
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit warning MVVMTK0030

Annotating a field with `[NotifyDataErrorInfo]` is not necessary if the containing type has or inherits `[NotifyDataErrorInfo]` at the class-level.

The following sample generates MVVMTK0030:

```csharp
using System.ComponentModel.DataAnnotations;
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[NotifyDataErrorInfo]
public partial class MyViewModel : ObservableValidator
{
    // Using [NotifyDataErrorInfo] is redundant here, as the
    // containing type is already annotated with the same attribute.
    [ObservableProperty]
    [Required]
    [NotifyDataErrorInfo]
    public int number;
}
```

The same applies if the class-level attribute is inherited:

```csharp
using System.ComponentModel.DataAnnotations;
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[NotifyDataErrorInfo]
public class MyBaseViewModel : ObservableValidator
{
}

public partial class MyViewModel : MyBaseViewModel
{
    // Using [NotifyPropertyChangedRecipients] is redundant here, as the
    // containing type is inheriting the same attribute from a base type.
    [ObservableProperty]
    [Required]
    [NotifyDataErrorInfo]
    public int number;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
