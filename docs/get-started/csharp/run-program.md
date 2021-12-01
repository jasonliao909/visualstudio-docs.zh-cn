---
title: 如何运行 C# 程序
description: 初学者指南介绍如何在 Visual Studio 中运行 C# 程序。
ms.custom: vs-acquisition, get-started
ms.date: 09/14/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: ghogen
ms.author: ghogen
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: f68039ca8b1bca3224766f7f2673514e3b6a2e9f
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128427964"
---
# <a name="how-to-run-a-c-program-in-visual-studio"></a>如何：在 Visual Studio 中运行 C# 程序

如何运行程序取决于你从什么开始执行、程序的类型，以及你是否想在调试器下运行。 最简单的是在 Visual Studio 中生成并运行一个打开的项目，在这种情况下，可执行以下操作：

- 按 F5，从 Visual Studio 菜单中选择“调试” > “开始执行(调试)”，或在 Visual Studio 工具栏上选择绿色的“开始”箭头和项目名称   。
- 你也可以按 Ctrl+F5，或从 Visual Studio 菜单中选择“调试” > “开始执行(不调试)”，直接运行而不调试   。

::: moniker range="<=vs-2019"
![显示“开始”按钮的屏幕截图。](media/vs-start-button.png)
::: moniker-end
::: moniker range=">=vs-2022"
:::image type="content" source="media/vs-2022/start-button.png" alt-text="显示“开始”按钮的屏幕截图。" border="false":::
::: moniker-end

## <a name="start-from-a-project"></a>从项目开始

你可以运行 C# 项目或 .csproj 文件（如果是可运行的程序）。 如果项目包含带有 `Main` 方法的 C# 文件，并且其输出为可执行文件（.exe 文件），则很可能会在项目成功生成后运行该文件。

1. 如果你的程序代码已在 Visual Studio 项目中，请打开该项目。 你可以执行以下操作来打开项目：双击或点击 Windows 文件资源管理器中的 .csproj 文件；或者在 Visual Studio 中选择“打开项目”，浏览以找到 .csproj 文件，然后选择该文件。

1. 在 Visual Studio 中加载项目后，如果 Visual Studio 解决方案包含多个项目，请确保将带有 `Main` 方法的项目设置为启动项目。 要设置启动项目，请右键单击“解决方案资源管理器”中的项目名称或节点，然后从上下文菜单中选择“设置为启动项目” 。

   ::: moniker range="<=vs-2019"
   ![显示设置启动项目的屏幕截图。](media/set-as-startup-project.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   :::image type="content" source="media/vs-2022/set-startup-project.png" alt-text="显示设置启动项目的屏幕截图。" border="false":::
   ::: moniker-end

1. 要运行程序，请按 Ctrl+F5，从顶部菜单中选择“调试” > “开始执行(不调试)”，或选择绿色的“开始”按钮    。 

   Visual Studio 会尝试生成并运行你的项目。 在 Visual Studio 屏幕的底部，生成输出显示在“输出”窗口中，生成错误显示在“错误列表”窗口中 。

   如果生成成功，应用会以适合项目类型的方式运行。 控制台应用在终端窗口中运行，Windows 桌面应用在新的桌面窗口中启动，Web 应用在由 IIS Express 承载的浏览器中运行。

## <a name="start-from-code"></a>从代码开始

如果是从代码清单、代码文件或少量文件开始，请首先确保该代码来自受信任的源，并且是可运行的程序。 带有 `Main` 方法的任何应用都可能是可运行的程序。 你可以使用“控制台应用程序”模板创建一个项目，以便在 Visual Studio 中使用该应用。

### <a name="code-listing-for-a-single-file"></a>单个文件的代码列表

1. 启动 Visual Studio，并打开一个空的 C# 控制台应用程序项目。
1. 将项目 .cs 文件中的所有代码替换为代码清单或文件的内容。
1. 将项目 .cs 文件重命名为与你的代码文件名一致。

### <a name="several-code-listings-or-files-on-disk"></a>磁盘上有多个代码清单或文件

1. 启动 Visual Studio，并创建适当类型的新项目。 如果不确定，请使用 C#“控制台应用程序”。
1. 在新项目中，将项目代码文件中的所有代码替换为第一个代码清单或文件的内容。
1. 重命名项目代码文件，使其与你的代码文件名一致。
1. 对于其余的每个代码文件：
   1. 右键单击“解决方案资源管理器”中的项目节点，然后选择“添加” > “现有项”，或选择该项目，然后按 Shift+Alt+A     。
   1. 浏览到并选择要导入到项目中的代码文件。

### <a name="several-files-in-a-folder"></a>文件夹中有多个文件

如果文件夹中有多个文件，请先查找项目或解决方案文件。 Visual Studio 创建的程序具有项目和解决方案文件。 在 Windows 文件资源管理器中，查找扩展名为 .csproj 或 .sln 的文件 。 双击 .csproj 文件，在 Visual Studio 中打开它。 请参阅[从 Visual Studio 解决方案或项目开始](#start-from-a-project)。

如果代码来自其他开发环境，则没有项目文件。 在 Visual Studio 中选择“打开” > “文件夹”，打开该文件夹 。 请参阅[开发代码而无需创建项目或解决方案](../../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)。

## <a name="start-from-a-github-or-azure-devops-repo"></a>从 GitHub 或 Azure DevOps 存储库开始

如果要运行的代码位于 GitHub 或 Azure DevOps 存储库中，则可以使用 Visual Studio 直接从存储库打开项目。 请参阅[打开存储库中的项目](../tutorial-open-project-from-repo.md)。

## <a name="run-the-program"></a>运行程序

要开始生成程序，请按 Visual Studio 工具栏上的绿色“开始”按钮，或者按 F5 或 Ctrl+F5   。 使用“开始”按钮或 F5 在调试器下运行程序 。

Visual Studio 会尝试在你的项目中生成并运行代码。 如果生成不成功，请参阅以下部分，了解有关如何成功生成项目的一些建议。

## <a name="troubleshooting"></a>疑难解答

你的代码可能有错误。 或者代码可能是正确的，但依赖于缺少的程序集或 NuGet 包，或者针对其他版本的 .NET。 在这些情况下，可以轻松地修复生成。

### <a name="add-references"></a>添加引用

要正确生成，代码必须正确，并具有对库或其他依赖项的正确引用。 代码中的红色波浪下划线或错误列表中的条目表明存在错误，即使在编译和运行程序之前也是如此。 如果错误与未解析的名称相关，则可能需要添加引用和/或 `using` 指令。 如果代码引用了任何缺失的程序集或 NuGet 包，则需要将这些引用添加到项目。

Visual Studio 会尝试帮助你识别缺少的引用。 如果名称未解析，编辑器中会出现灯泡图标。 选择灯泡，可以看到有关如何修复此问题的一些建议。 解决方法可能是：

- 添加 using 指令。
- 添加对程序集的引用。
- 安装 NuGet 包。

#### <a name="add-a-using-directive"></a>添加 using 指令

下面是缺少的 `using` 指令的示例。 你可以将 `using System;` 添加到代码文件的开头，以解析无法解析的名称 `Console`：

::: moniker range="<=vs-2019"
![添加 using 指令的灯泡的屏幕截图。](media/name-does-not-exist2.png)
::: moniker-end
::: moniker range=">=vs-2022"
:::image type="content" source="media/vs-2022/missing-using-directive.png" alt-text="添加 using 指令的灯泡的屏幕截图。" border="false":::
::: moniker-end

#### <a name="add-an-assembly-reference"></a>添加程序集引用

.NET 引用可以是程序集或 NuGet 包。 在源代码中，发布者或作者通常会说明代码所需的程序集以及它所依赖的包。 要手动添加对项目的引用，请右键单击“解决方案资源管理器”中的“引用”节点，然后选择“添加引用”  。 在“引用管理器”中，找到并添加所需的程序集。

::: moniker range="<=vs-2019"
![“添加引用”菜单的屏幕截图。](media/add-reference.png)
::: moniker-end
::: moniker range=">=vs-2022"
:::image type="content" source="media/vs-2022/add-reference.png" alt-text="“添加引用”菜单的屏幕截图。" border="false":::
::: moniker-end

你可以按照[使用引用管理器添加或删除引用](../../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md)中的说明查找程序集并添加引用。

#### <a name="add-a-nuget-package"></a>添加 NuGet 包

如果 Visual Studio 检测到缺少 NuGet 包，则会显示一个灯泡，并提供安装包的选项：

::: moniker range="<=vs-2019"
![安装 NuGet 包的灯泡的屏幕截图。](media/lightbulb-add-package.png)
::: moniker-end
::: moniker range=">=vs-2022"
:::image type="content" source="media/vs-2022/lightbulb-add-package.png" alt-text="安装 NuGet 包的灯泡的屏幕截图。" border="false":::
::: moniker-end

如果这不能解决问题，或者 Visual Studio 找不到包，请尝试联机搜索包。 请参阅[在 Visual Studio 中安装和使用 NuGet 包](/nuget/quickstart/install-and-use-a-package-in-visual-studio)。

### <a name="use-the-right-version-of-net"></a>使用正确版本的 .NET

由于不同版本的 .NET Framework 具有一定的后向兼容性，因此较新的框架可能会运行针对较旧的框架编写的代码，且不需要进行任何更改。 但有时则需要针对特定的 .NET Framework 版本。 你可能需要安装特定版本的 .NET Framework 或 .NET Core。 请参阅[修改 Visual Studio](../../install/modify-visual-studio.md)。

要更改目标 .NET Framework 版本，请参阅[更改目标框架](../../ide/visual-studio-multi-targeting-overview.md#select-a-target-framework-version)。 有关详细信息，请参阅 [.NET Framework 目标错误疑难解答](../../msbuild/troubleshooting-dotnet-framework-targeting-errors.md)。

## <a name="next-steps"></a>后续步骤

- 阅读[欢迎使用 Visual Studio IDE](../visual-studio-ide.md)，探索 Visual Studio 开发环境。
- [创建自己的第一个 C# 应用](tutorial-console.md)
