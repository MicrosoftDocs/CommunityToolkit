---
title: MVVM Toolkit warning MVVMTK0049
author: Sergio0694
description: MVVM Toolkit warning MVVMTK0049
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit warning MVVMTK0049

Using the `[INotifyPropertyChanged]` attribute on types is not AOT compatible in WinRT scenarios (such as UWP XAML and WinUI 3 apps), and they should derive from `ObservableObject` or manually implement `INotifyPropertyChanged` instead (as it allows the CsWinRT generators to correctly produce the necessary WinRT marshalling code).

The following sample generates MVVMTK0049:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[INotifyPropertyChanged]
public partial class SampleViewModel
{    
}
```

You should instead derive from `ObservableObject`:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{    
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
