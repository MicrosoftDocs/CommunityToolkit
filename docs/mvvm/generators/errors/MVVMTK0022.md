---
title: MVVM Toolkit error MVVMTK0022
author: Sergio0694
description: MVVM Toolkit error MVVMTK0022
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0022

Fields annotated with `[NotifyPropertyChangedRecipients]` must be contained in a type that inherits from `ObservableRecipient` or that is annotated with `[ObservableRecipient]` (including base types).

The following sample generates MVVMTK0022:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class MyViewModel : ObservableObject
{
    // The containing type does not have the ObservableRecipient functionality
    [ObservableProperty]
    [NotifyPropertyChangedRecipients]
    public int number;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
