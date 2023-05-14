---
title: MVVM Toolkit warning MVVMTKCFG0002
author: Sergio0694
description: MVVM Toolkit warning MVVMTKCFG0002
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit warning MVVMTKCFG0002

This warning is produced by the .targets file bundled with the MVVM Toolkit, whenever a project referencing the library is using [packages.config](https://learn.microsoft.com/nuget/reference/packages-config) to resolve NuGet packages. In this case, the MVVM Toolkit source generators will not be loaded correctly by Roslyn, and will not be usable. The MVVM Toolkit itself will work just fine, but features relying on the source generators will not be available.

It is recommended to migrate to using `<PackageReference>`, which will also resolve this issue.

You can consult the [official migration documentation](https://learn.microsoft.com/nuget/consume-packages/migrate-packages-config-to-package-reference) to help with this.
