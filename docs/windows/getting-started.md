---
title: Getting Started with the Windows Community Toolkit
author: michael-hawker
description: Overview of how to get started with the Windows Community Toolkit to build amazing Windows apps
keywords: windows 10, windows 11, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, windowsappsdk, wasdk, winui2, winui3, winui, uno platform
ms.date: 09/07/2023
---

# Get started

This article covers how to get started using the packages provided as part of the Windows Community Toolkit project.

## Adding the NuGet package(s)

The toolkit is available as a set of NuGet packages that can be added to any existing or new project using Visual Studio.

1. Open an existing project, or create a new project for the framework you're working with:

   - [UWP - WinUI2](/windows/apps/winui/winui2/getting-started)
   - [WindowsAppSDK - WinUI3](/windows/apps/winui/winui3/create-your-first-winui3-app)
   - [Uno Platform](https://platform.uno/docs/articles/get-started-vs-2022.html)

2. In the Solution Explorer panel, right click on your project name and select **Manage NuGet Packages**.

    For _UWP/WinUI2 or Uno.UI_ based projects, search for **CommunityToolkit.Uwp**, and choose the desired NuGet Package from the list.

    For _Windows App SDK/WinUI3 or Uno.WinUI_ based projects, search for **CommunityToolkit.WinUI** instead.

    ![Manage NuGet Packages...](../images/get-started/manage-nuget-packages.png "Right click on the solution and select 'Manage NuGet Packages...'")

3. Choose the components that are most appropriate for your needs from the list and install.

    You can see the available component packages listed on the left-hand table-of-contents.

4. Regardless of the package/framework you're using, namespaces will begin with `CommunityToolkit.WinUI`.

## Other Resources

Download the [Windows Community Toolkit Gallery](https://aka.ms/windowstoolkitapp) from the Windows store to see the controls in an actual app.

Visit the [Windows Community Toolkit Github Repository](https://aka.ms/toolkit/windows) to see the current source code, what is coming next, and clone the repository. Community contributions are welcome! If you have an idea for a new feature, check out [Windows Community Toolkit Labs](https://aka.ms/toolkit/labs/windows) for the latest experiments and process for proposing new features.
