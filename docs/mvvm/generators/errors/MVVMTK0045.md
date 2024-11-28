---
title: MVVM Toolkit warning MVVMTK0045
author: Sergio0694
description: MVVM Toolkit warning MVVMTK0045
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit warning MVVMTK0045

Fields using `[ObservableProperty]` will generate code that is not AOT compatible in WinRT scenarios (such as UWP XAML and WinUI 3 apps), and partial properties should be used instead (as they allow the CsWinRT generators to correctly produce the necessary WinRT marshalling code).

The following sample generates MVVMTK0045:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    private string? name;
}
```

You should instead make that field a partial property (eg. named `Name`), like so:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    public partial string? Name { get; set; }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
