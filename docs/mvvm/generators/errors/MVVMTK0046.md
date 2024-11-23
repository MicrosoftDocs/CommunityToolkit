---
title: MVVM Toolkit warning MVVMTK0046
author: Sergio0694
description: MVVM Toolkit warning MVVMTK0046
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit warning MVVMTK0046

Using `[RelayCommand]` on methods within a type also using `[GeneratedBindableCustomProperty]` is not supported, and a manually declared command property should be used instead (the `[GeneratedBindableCustomProperty]` generator cannot see the generated command property that is produced by the MVVM Toolkit generator).

The following sample generates MVVMTK0046:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

[GeneratedBindableCustomProperty]
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

[GeneratedBindableCustomProperty]
public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    public partial string? Name { get; set; }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
