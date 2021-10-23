---
title: 并排安装 Visual Studio 版本
description: 了解如何在已安装 Visual Studio 早期版本或更高版本的计算机上安装 Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 03/29/2021
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: conceptual
helpviewer_keywords:
- side-by-side installations [Visual Studio]
- Help [Visual Studio], installing
- install multiple versions of Visual Studio
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.openlocfilehash: a4df127d6131f6121c68f9900f2af8a3f66da811
ms.sourcegitcommit: 0257750be796cc46e01cebd8976f637743d29417
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2021
ms.locfileid: "130290637"
---
# <a name="install-visual-studio-versions-side-by-side"></a>并排安装 Visual Studio 版本

你可以在已安装 Visual Studio 早期版本或更高版本的计算机上安装 Visual Studio。

::: moniker range="vs-2017"

在并行安装各版本之前，你应了解以下情况：

* 如果使用 Visual Studio 2017 打开在 Visual Studio 2015 中创建的解决方案，则稍后可以在旧版本中再次打开和修改该解决方案，前提是你没有执行任何 Visual Studio 2017 特有的功能。

* 如果你尝试使用 Visual Studio 2017 打开在 Visual Studio 2015 或更早的版本中创建的解决方案，则可能需要修改你的项目和文件才能与 Visual Studio 2017 兼容。 有关详细信息，请参阅[移植、迁移和升级 Visual Studio 项目](../porting/port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2017&preserve-view=true)页。

::: moniker-end

::: moniker range="vs-2019"

在并行安装各版本之前，你应了解以下情况：

* 如果使用 Visual Studio 2019 打开在 Visual Studio 2017 中创建的解决方案，则稍后可以在旧版本中再次打开和修改该解决方案，前提是你没有执行任何 Visual Studio 2019 特有的功能。

* 如果你尝试使用 Visual Studio 2019 打开在 Visual Studio 2017 或更早的版本中创建的解决方案，则可能需要修改你的项目和文件才能与 Visual Studio 2019 兼容。 有关详细信息，请参阅[移植、迁移和升级 Visual Studio 项目](../porting/port-migrate-and-upgrade-visual-studio-projects.md)页。

::: moniker-end

::: moniker range=">=vs-2022"

在并行安装各版本之前，你应了解以下情况：

* 如果使用 Visual Studio 2022 打开在 Visual Studio 2017 或 Visual Studio 2019 中创建的解决方案，则稍后可以在旧版本中再次打开和修改该解决方案，前提是你没有执行任何 Visual Studio 2022 特有的功能。

* 如果你尝试使用 Visual Studio 2022 打开在 Visual Studio 2019 或更早的版本中创建的解决方案，则可能需要修改你的项目和文件才能与 Visual Studio 2022 兼容。 有关详细信息，请参阅[移植、迁移和升级 Visual Studio 项目](../porting/port-migrate-and-upgrade-visual-studio-projects.md)页。

::: moniker-end

* 如果在已安装多个版本的计算机上卸载 Visual Studio 的一个版本，则将为所有版本移除 Visual Studio 的文件关联。

* 因为并非所有扩展都兼容，所以 Visual Studio 不会自动升级扩展。 必须从 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) 或软件发行者处重新安装扩展。

## <a name="install-minor-visual-studio-versions-side-by-side"></a>并行安装 Visual Studio 次要版本

从 Visual Studio 的一个次要版本升级到下一个版本时，Visual Studio 安装程序默认会将当前安装版本更新为该通道中的最新版本。 例如，假设刚刚发布了 16.9.4。 安装程序将尝试替换当前安装的 16.9.3（或更低版本）和 16.9.4，因为这两个版本都是 [Visual Studio 2019 发布通道](/visualstudio/productinfo/release-rhythm)的一部分。 在更新期间将旧版本替换为新版本有助于确保较早版本的 Visual Studio 不会占用计算机上的空间。 但是，在某些特定情况下，并行安装不同次要版本的 Visual Studio 可能会有所帮助。 例如，你可能想要在同一台计算机上同时具备 16.9.3 和16.9.4。

::: moniker range="vs-2017"

1. 从要与现有 Visual Studio 版本并行安装的版本的 [Visual Studio 早期版本](https://visualstudio.microsoft.com/vs/older-downloads/)页下载 Visual Studio 2017 版本 15.9 的最新引导程序。

1. 在管理员模式下打开命令提示符。 为此，请打开 Windows“开始”菜单，键入“cmd”，右键单击命令提示符搜索结果，然后选择“以管理员身份运行”。 在命令提示符中，将目录更改为 Visual Studio 引导程序文件所在的文件夹。

1. 运行以下命令，为安装位置指定一个新文件夹路径，并将 .exe 文件名替换为要安装的 Visual Studio 版本的相应引导程序名称。 .exe 文件名应与以下文件名之一匹配或类似：

   * 对于 Visual Studio Enterprise，应与 vs_enterprise.exe 匹配或类似
   * 对于 Visual Studio Professional，应与 vs_professional.exe 匹配或类似

1. 按照安装程序对话框选择安装所需的组件。 有关详细信息，请参阅[安装 Visual Studio](install-visual-studio.md#step-4---choose-workloads)。

::: moniker-end

::: moniker range="vs-2019"

1. 从要与现有 Visual Studio 版本并行安装的次要版本的 [Visual Studio 下载页](https://visualstudio.microsoft.com/downloads)或 [Visual Studio 2019 版本](/visualstudio/releases/2019/history#installing-an-earlier-release)页下载 Visual Studio 2019 引导程序文件。

1. 在管理员模式下打开命令提示符。 为此，请打开 Windows“开始”菜单，键入“cmd”，右键单击命令提示符搜索结果，然后选择“以管理员身份运行”。 在命令提示符中，将目录更改为 Visual Studio 引导程序文件所在的文件夹。

1. 运行以下命令，为安装位置指定一个新文件夹路径，并将 .exe 文件名替换为要安装的 Visual Studio 版本的相应引导程序名称。 .exe 文件名应与以下文件名之一匹配或类似：

   * 对于 Visual Studio Enterprise，应与 vs_enterprise.exe 匹配或类似
   * 对于 Visual Studio Professional，应与 vs_professional.exe 匹配或类似
   * 对于 Visual Studio Community，应与 vs_community.exe 匹配或类似

   ```shell
   vs_Enterprise.exe --installPath "C:\Program Files (x86)\Microsoft Visual Studio\<AddNewPath>"
   ```

1. 按照安装程序对话框选择安装所需的组件。 有关详细信息，请参阅[安装 Visual Studio](install-visual-studio.md#step-4---choose-workloads)。

::: moniker-end

::: moniker range=">=vs-2022"

1. 从要与现有 Visual Studio 版本并行安装的次要版本的 [Visual Studio 下载页](https://visualstudio.microsoft.com/downloads)或 [Visual Studio 2022 版本](/visualstudio/releases/2022/release-notes)页下载 Visual Studio 2022 引导程序文件。

1. 在管理员模式下打开命令提示符。 为此，请打开 Windows“开始”菜单，键入“cmd”，右键单击命令提示符搜索结果，然后选择“以管理员身份运行”。 在命令提示符中，将目录更改为 Visual Studio 引导程序文件所在的文件夹。

1. 运行以下命令，为安装位置指定一个新文件夹路径，并将 .exe 文件名替换为要安装的 Visual Studio 版本的相应引导程序名称。 .exe 文件名应与以下文件名之一匹配或类似：

   * 对于 Visual Studio Enterprise，应与 vs_enterprise.exe 匹配或类似
   * 对于 Visual Studio Professional，应与 vs_professional.exe 匹配或类似
   * 对于 Visual Studio Community，应与 vs_community.exe 匹配或类似

   ```shell
   vs_Enterprise.exe --installPath "C:\Program Files\Microsoft Visual Studio\<AddNewPath>"
   ```

1. 按照安装程序对话框选择安装所需的组件。 有关详细信息，请参阅[安装 Visual Studio](install-visual-studio.md#step-4---choose-workloads)。
   
::: moniker-end

## <a name="net-framework-versions-and-side-by-side-installations"></a>.NET Framework 版本和并行安装

Visual Basic、Visual C# 和 Visual F# 项目使用“项目设计器”中的“目标框架”选项来指定项目使用的 .NET Framework 版本 。 对于 C++ 项目，您可以通过修改 .vcxproj 文件手动更改目标框架。 有关详细信息，请参阅 [.NET Framework 的版本兼容性](/dotnet/framework/migration-guide/version-compatibility)页。

创建项目时，可以在 **“新建项目”** 对话框中的 **“.NET Framework”** 列表中指定项目针对的 .NET Framework 版本。

有关语言特定的信息，请参见下表中的相应主题。

::: moniker range="vs-2017"

| 语言     | 主题                                                                                                                                                   |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| Visual Basic | [“项目设计器”->“应用程序”页 (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md?view=vs-2017&preserve-view=true) |
| Visual C#    | [“项目设计器”->“应用程序”页 (C#)](../ide/reference/application-page-project-designer-csharp.md?view=vs-2017&preserve-view=true)                 |
| Visual F#    | [在 Visual Studio 中使用 Visual F# 进行开发](../ide/fsharp-visual-studio.md?view=vs-2017&preserve-view=true)                                               |
| C++          | [如何：修改目标框架和平台工具集](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset/)                         |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md?view=vs-2017&preserve-view=true)
* [移植、迁移和升级 Visual Studio 项目](../porting/port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2017&preserve-view=true)
* [生成 C/C++ 独立应用程序和并行程序集](/cpp/build/building-c-cpp-isolated-applications-and-side-by-side-assemblies/)

::: moniker-end

::: moniker range=">= vs-2019"

| 语言     | 主题                                                                                                                           |
|--------------|---------------------------------------------------------------------------------------------------------------------------------|
| Visual Basic | [“项目设计器”->“应用程序”页 (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)         |
| Visual C#    | [“项目设计器”->“应用程序”页 (C#)](../ide/reference/application-page-project-designer-csharp.md)                         |
| Visual F#    | [在 Visual Studio 中使用 Visual F# 进行开发](../ide/fsharp-visual-studio.md)                                                       |
| C++          | [如何：修改目标框架和平台工具集](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset/) |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md)
* [移植、迁移和升级 Visual Studio 项目](../porting/port-migrate-and-upgrade-visual-studio-projects.md)
* [生成 C/C++ 独立应用程序和并行程序集](/cpp/build/building-c-cpp-isolated-applications-and-side-by-side-assemblies/)

::: moniker-end
