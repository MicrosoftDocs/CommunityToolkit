---
title: MVVM Toolkit error MVVMTK0035
author: Sergio0694
description: MVVM Toolkit error MVVMTK0035
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0035

All attributes targeting the generated property for a field annotated with `[ObservableProperty]` must correctly be resolved to valid types. This error is shown when a given `property:` attribute over a field with `[ObservableProperty]` is not correctly resolved to a type, which helps identifying issues at compile time as soon as possible. A common example where this can happen is if a `using` directive for the attribute is missing.

The following sample generates MVVMTK0035:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    [property: JsonPropertyName("name")]
    private string? name;
}
```

You can see that `JsonPropertyName` has no `using` directive here, and as such is not resolved correctly. You can fix this by updating the code as follows:

```csharp
using System.Text.Json.Serialization;
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    [ObservableProperty]
    [property: JsonPropertyName("name")]
    private string? name;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
