---
title: MVVM Toolkit error MVVMTK0015
author: Sergio0694
description: MVVM Toolkit error MVVMTK0015
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0015

The target(s) of `[NotifyPropertyChangedFor]` must be a (different) accessible property in its parent type.

The following sample generates MVVMTK0015:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    // The containing type has no property named "FooBar"
    [ObservableProperty]
    [NotifyPropertyChangedFor("FooBar")]
    private string name;
}
```

The same applies if the property name is just `null`:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    // The target property name is invalid (cannot be null)
    [ObservableProperty]
    [NotifyPropertyChangedFor(null)]
    private string name;
}
```

Additionally, the type of target member is validated as well:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class SampleViewModel : ObservableObject
{
    // The target member "Foo" should be a property, but it's a method
    [ObservableProperty]
    [NotifyPropertyChangedFor(nameof(Foo))]
    private string name;

    public void Foo()
    {
    }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
