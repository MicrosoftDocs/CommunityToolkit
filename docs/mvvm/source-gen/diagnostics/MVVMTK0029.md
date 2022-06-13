---
title: MVVM Toolkit warning MVVMTK0029
author: Sergio0694
description: MVVM Toolkit warning MVVMTK0029
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit warning MVVMTK0029

Annotating a field with `[NotifyPropertyChangedRecipients]` is not necessary if the containing type has or inherits `[NotifyPropertyChangedRecipients]` at the class-level.

The following sample generates MVVMTK0029:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[NotifyPropertyChangedRecipients]
public partial class MyViewModel : ObservableRecipient
{
    // Using [NotifyPropertyChangedRecipients] is redundant here, as the
    // containing type is already annotated with the same attribute.
    [ObservableProperty]
    [NotifyPropertyChangedRecipients]
    public int number;
}
```

The same applies if the class-level attribute is inherited:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[NotifyPropertyChangedRecipients]
public class MyBaseViewModel : ObservableRecipient
{
}

public partial class MyViewModel : MyBaseViewModel
{
    // Using [NotifyPropertyChangedRecipients] is redundant here, as the
    // containing type is inheriting the same attribute from a base type.
    [ObservableProperty]
    [NotifyPropertyChangedRecipients]
    public int number;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
