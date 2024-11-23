---
title: MVVM Toolkit error MVVMTK0044
author: Sergio0694
description: MVVM Toolkit error MVVMTK0044
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0044

Using `[ObservableProperty]` with (partial) properties requires a higher version of Roslyn (remove `[ObservableProperty]` or target a field instead, or upgrade to at least Visual Studio 2022 version 17.12 and the .NET 9 SDK).

The following sample generates MVVMTK0044 when using an older .NET SDK (eg. the .NET 8 SDK):

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    public partial string? Name { get; set; }
}
```

You should update your environment to Visual Studio 17.12 and the .NET 9 SDK.

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
