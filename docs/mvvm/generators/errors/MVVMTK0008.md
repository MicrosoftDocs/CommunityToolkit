---
title: MVVM Toolkit error MVVMTK0008
author: Sergio0694
description: MVVM Toolkit error MVVMTK0008
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit error MVVMTK0008

The source generator features from the MVVM Toolkit require consuming projects to set the C# language version to at least C# 8.0. Make sure to add `<LangVersion>8.0</LangVersion>` (or above) to your .csproj file.

To learn more about how to enable a newer C# version on older frameworks, [see this blog post](https://sergiopedri.medium.com/enabling-and-using-c-9-features-on-older-and-unsupported-runtimes-ce384d8debb).

> [!NOTE]
> While updating the C# language version will generally work with no issues, as the compiler has to be resilient to missing types and runtime features, using a newer C# version than the default one for a given framework/runtime is not officially supported. Make sure to test your application properly if you decide to manually override the language version in your projects.

The following sample generates MVVMTK0008:

```xml
<PropertyGroup>
    <LangVersion>7.3</LangVersion>
</PropertyGroup>
```
```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace MyApp;

// The project doesn't have a high enough version of C#
[INotifyPropertyChanged]
public partial class SampleViewModel
{
}
```

## Additional resources

- You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Mvvm.SourceGenerators.UnitTests).
