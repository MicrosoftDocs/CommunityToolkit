---
title: MVVM Toolkit warning MVVMTK0034
author: Sergio0694
description: MVVM Toolkit warning MVVMTK0034
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit warning MVVMTK0034

Fields with [ObservableProperty] should not be directly referenced, and the generated properties should be used instead. This warning exists to help avoid cases where developers accidentally refer to backing fields of a generated property to update its value, and then see no property change notification being raised. The generated property should always be referenced instead.

The following sample generates MVVMTK0034:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    private string? name;

    public void UpdateName()
    {
        name = Database.LoadUsername();
    }
}
```

And you can fix it by updating the code as follows:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    private string? name;

    public void UpdateName()
    {
        Name = Database.LoadUsername();
    }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
