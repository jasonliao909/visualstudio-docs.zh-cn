---
title: 安装第三方分析器
ms.date: 08/27/2020
description: 了解如何在 Visual Studio 中安装第三方分析Visual Studio。 了解如何在 .vsix 文件和分析器包NuGet分析器。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: a31fbbc8a0e655418425416ffdcae3aa16810788
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601285"
---
# <a name="install-third-party-analyzers"></a>安装第三方分析器

Visual Studio包括 *Roslyn .NET Compiler Platform (分析器)* 核心集。 这些分析器始终打开。 可以安装其他分析器作为NuGet包，也可以作为 *VSIX* Visual Studio扩展安装。

## <a name="to-install-nuget-analyzer-packages"></a>安装 NuGet 分析器包

1. 找到要安装在 www.nuget.org 上的分析器 www.nuget.org。

   例如，你可能想要安装 [StyleCop.Analyzers](https://www.nuget.org/packages/stylecop.analyzers/) 来查找代码库中的样式问题。

2. 使用 Visual Studio 控制台或 程序包管理器[UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)在 程序包管理器[中安装包](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)。

   > [!NOTE]
   > 每个 www.nuget.org 包的"输出"页显示要粘贴到控制台 程序包管理器 **的命令**。 甚至还有一个方便按钮，用于将文本复制到剪贴板。

   分析器程序集已安装，并 **出现在解决方案资源管理器****分析器**  >  **下**。

## <a name="to-install-vsix-analyzers"></a>安装 VSIX 分析器

::: moniker range="vs-2017"

1. 在Visual Studio"中，选择 **"工具** > **扩展和更新"。**

   此时，“扩展和更新”对话框打开。

   > [!NOTE]
   > 或者，可以直接从市场 找到并下载Visual Studio[扩展](https://marketplace.visualstudio.com)。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在Visual Studio中，**选择"扩展** > **""管理扩展"。**

   " **管理扩展"** 对话框随即打开。

   > [!NOTE]
   > 或者，可以直接从市场 找到并下载Visual Studio[扩展](https://marketplace.visualstudio.com)。

::: moniker-end

2. 在 **左窗格中** 展开"联机"，然后选择 **"Visual Studio市场"。**

3. 在搜索框中，键入要安装的分析器扩展的名称。

4. 选择“下载”  。

   扩展已下载。

5. 选择 **"** 确定"以关闭对话框，然后关闭 Visual Studio以启动 **VSIX 安装程序**。

   **"VSIX 安装程序**"对话框随即打开。

   ![适用于 Microsoft Code Analysis 的 VSIX 安装程序](media/vsix-installer-code-analysis.png)

6. 选择 **"修改** "以开始安装。

7. 一两分钟后，安装完成。 选择“关闭”  。

8. 再次Visual Studio打开。

::: moniker range="vs-2017"

如果要检查是否已安装扩展，请选择"工具  >  **扩展和更新"。** 在"**扩展和更新"** 对话框中，选择左侧的"已安装"类别，然后按名称搜索扩展。

::: moniker-end

::: moniker range=">=vs-2019"

如果要检查扩展是否已安装，请选择"扩展  >  **""管理扩展"。** 在 **"管理扩展"** 对话框中，选择左侧的" **已安装** "类别，然后按名称搜索扩展。

::: moniker-end

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [在 Visual Studio 中使用代码分析器](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>请参阅

- [中代码分析器Visual Studio](../code-quality/roslyn-analyzers-overview.md)
- [安装 .NET 分析器](../code-quality/install-net-analyzers.md)
