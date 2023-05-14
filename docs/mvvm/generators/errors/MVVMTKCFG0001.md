---
title: MVVM Toolkit warning MVVMTKCFG0001
author: Sergio0694
description: MVVM Toolkit warning MVVMTKCFG0001
keywords: community toolkit, dotnet, csharp, mvvm, net core, net standard, source generators
dev_langs:
  - csharp
---

# MVVM Toolkit warning MVVMTKCFG0001

This warning is produced by the .targets file bundled with the MVVM Toolkit, whenever a project referencing the library is using an older version of Roslyn (eg. Roslyn 3.x), which does not support the source generators. In this case, all MVVM Toolkit source generators will be disabled. The MVVM Toolkit itself will work just fine, but features relying on the source generators will not be available.

You can obtain a recent version of Roslyn via:
- Manually installing a recent version of the .NET SDK (https://get.dot.net)
- Installing a recent version of Visual Studio 2022+ (https://visualstudio.microsoft.com/)
- Installing another IDE (eg. Rider) with a modern bundled toolset
