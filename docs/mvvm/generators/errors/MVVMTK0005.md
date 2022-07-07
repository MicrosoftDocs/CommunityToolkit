---
title: MVVM Toolkit error MVVMTK0005
author: Sergio0694
description: MVVM Toolkit error MVVMTK0005
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0005

Cannot apply `[ObservableRecipient]` to a type that lacks necessary base functionality (it should either inherit from `ObservableObject`, or be annotated with `[ObservableObject]` or `[INotifyPropertyChanged]`).

The following sample generates MVVMTK0005:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

// The type lacks a base implementation of INotifyPropertyChanged
[ObservableRecipient]
public partial class SampleViewModel
{
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
