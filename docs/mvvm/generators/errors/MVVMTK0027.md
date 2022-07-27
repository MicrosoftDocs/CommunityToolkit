---
title: MVVM Toolkit error MVVMTK0027
author: Sergio0694
description: MVVM Toolkit error MVVMTK0027
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0027

Types annotated with `[NotifyPropertyChangedRecipients]` must inherit from `ObservableRecipient` or be annotated with `[ObservableRecipient]` (including base types).

The following sample generates MVVMTK0027:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

// This type is requesting broadcast support but doesn't have ObservableRecipient features
[NotifyPropertyChangedRecipients]
public partial class MyViewModel : ObservableObject
{
    [ObservableProperty]
    public int number;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
