---
title: MVVM Toolkit error MVVMTK0024
author: Sergio0694
description: MVVM Toolkit error MVVMTK0024
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0024

The fields annotated with `[ObservableProperty]` cannot result in a property name or have a type that would cause conflicts with other generated members.

The following sample generates MVVMTK0024:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

public partial class MyViewModel : ObservableObject
{
    // This field would generate a property named "Property", which would cause the
    // generated partial OnPropertyChanged() method to collide with the base helper
    // method to raise the PropertyChanged event. Additionally, since the field is
    // of type object, this would make the generated OnPropertyChanged() call bind
    // to the generated partial method, and not to the helper raising the event.
    [ObservableProperty]
    public object property;
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
