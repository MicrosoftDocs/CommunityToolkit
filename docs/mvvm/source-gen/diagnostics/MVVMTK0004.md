---
title: MVVM Toolkit error MVVMTK0004
author: Sergio0694
description: MVVM Toolkit error MVVMTK0004
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0004

Cannot apply `[ObservableRecipient]` to a type that already inherits from the `ObservableRecipient` class.

The following sample generates MVVMTK0004:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

// The type already inherits from ObservableRecipient
[ObservableRecipient]
public partial class SampleViewModel : ObservableRecipient
{
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
