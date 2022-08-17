---
title: MVVM Toolkit error MVVMTK0020
author: Sergio0694
description: MVVM Toolkit error MVVMTK0020
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0020

Fields not annotated with `[ObservableProperty]` cannot use `[NotifyPropertyChangedFor]`, `[NotifyCanExecuteChangedFor]`, `[NotifyPropertyChangedRecipients]` and `[NotifyDataErrorInfo]`.

The following sample generates MVVMTK0020:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class MyViewModel
{
    // The field is not using [ObservableProperty]
    [NotifyPropertyChangedFor("")]
    public int number;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
