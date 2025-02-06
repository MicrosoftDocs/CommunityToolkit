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
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

[GeneratedBindableCustomProperty]
public partial class SampleViewModel
{
    [RelayCommand]
    private void DoWork()
    {      
    }
}
```

You should instead make that field a partial property (eg. named `Name`), like so:

```csharp
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

[GeneratedBindableCustomProperty]
public partial class SampleViewModel
{
    private IRelayCommand? doWorkCommand;

    public IRelayCommand DoWorkCommand => doWorkCommand ??= new RelayCommand(DoWork);

    private void DoWork()
    {      
    }
}
```

If you're using Visual Studio 17.12 or above, and C# preview, you can also do this instead:

```csharp
using CommunityToolkit.Mvvm.Input;

namespace MyApp;

[GeneratedBindableCustomProperty]
public partial class SampleViewModel
{
    public IRelayCommand DoWorkCommand => field ??= new RelayCommand(DoWork);

    private void DoWork()
    {      
    }
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
