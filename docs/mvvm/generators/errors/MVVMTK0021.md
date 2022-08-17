---
title: MVVM Toolkit error MVVMTK0021
author: Sergio0694
description: MVVM Toolkit error MVVMTK0021
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0021

Cannot apply `[ObservableRecipient]` to a type that already inherits this attribute from a base type.

The following sample generates MVVMTK0021:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[ObservableRecipient]
public partial class A : ObservableObject
{
}

// The base type is already using [ObservableRecipient]
[ObservableRecipient]
public partial class B : A
{
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
