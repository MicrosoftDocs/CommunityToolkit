---
title: MVVM Toolkit warning MVVMTK0032
author: Sergio0694
description: MVVM Toolkit warning MVVMTK0032
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit warning MVVMTK0032

Classes with no base types should prefer inheriting from `ObservableObject` instead of using attributes to generate `INotifyPropertyChanged` code, as that will reduce the binary size of the application (the attributes are only meant to support cases where the annotated types are already inheriting from a different type). This diagnostic applies to cases where `[INotifyPropertyChanged]` is used in particular.

The following sample generates MVVMTK0032:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[INotifyPropertyChanged]
public partial class SampleViewModel
{
}
```

And you can fix it by updating the code as follows:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
