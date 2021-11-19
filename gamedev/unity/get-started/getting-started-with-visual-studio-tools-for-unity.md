---
title: Visual Studio Tools for Unity 入门 | Microsoft Docs
description: 了解如何安装和设置 Unity Visual Studio的安装程序。
ms.date: 01/27/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: how-to
ms.assetid: 66b5b4eb-13b5-4071-98d2-87fafa4598a8
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
zone_pivot_groups: platform
ms.openlocfilehash: c7daa1d99741cee9a480bfd2108ee093107ab58c
ms.sourcegitcommit: aaa3146356421d921714c29ffd586083570ade3d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2021
ms.locfileid: "129635628"
---
# <a name="get-started-with-visual-studio-and-unity"></a>Visual Studio Unity 入门

> [!NOTE]
> 本指南假定你已使用 Unity 中心程序安装了 Unity。 如果对 Unity 很了解，建议先访问 Unity Learn 并完成 [Unity Essentials 学习](https://learn.unity.com/pathway/unity-essentials) 路径。

## <a name="install-unity-support-for-visual-studio"></a>安装 Unity 对 Visual Studio

Visual Studio Tools for Unity是一个免费扩展，它支持编写和调试 C# 等。 有关 [扩展包括内容](./visual-studio-tools-for-unity.md) 的完整列表，请访问 Tools for Unity 概述。

:::zone pivot="windows"

> [!NOTE]
> 此安装指南适用于Visual Studio。 如果使用的是 Visual Studio Code，请访问[Unity 开发VS Code文档](https://code.visualstudio.com/docs/other/unity)。

1. [下载Visual Studio安装程序](/visualstudio/install/install-visual-studio)，或运行它（如果已安装）。
2. 为所需的 Visual Studio 版本单击“修改”（如已安装）或“安装”（适用于新安装）。
3. 在" **工作负载"** 选项卡上，滚动到 **"游戏"部分** ，然后选择"使用 **Unity 的游戏开发"** 工作负载。

    ![安装程序中的"使用 Unity 工作负载进行游戏开发"框](../media/vs/unity-workload.png)

:::zone-end
:::zone pivot="macos"

> [!NOTE]
> 此安装指南适用于Visual Studio for Mac。 如果使用的是 Visual Studio Code，请访问[Unity 开发VS Code文档](https://code.visualstudio.com/docs/other/unity)。

Unity 工具包含在安装 Visual Studio for Mac无需单独的安装步骤。 可以在"游戏开发"Visual Studio for Mac >**扩展>对此进行验证**。 **Visual Studio for Mac Unity 工具**" 。

![显示已启用 Visual Studio for Mac Tools for Unity 的扩展管理器视图](../media/vsm/unity-workload.png)

:::zone-end

## <a name="check-for-updates"></a>检查更新

建议保持更新Visual Studio Visual Studio for Mac，以便获得最新的 bug 修复、功能和 Unity 支持。 这不需要更新 Unity 版本。

:::zone pivot="windows"

1. 单击" **帮助>检查更新"** 菜单。

    ![2019 年 1 月中的"检查Visual Studio"菜单](../media/vs/check-for-updates.png)

2. 如果有可用的更新，则Visual Studio 安装程序会显示新版本。 单击“更新”按钮。

:::zone-end
:::zone pivot="macos"

1. 单击 **"Visual Studio for Mac >检查更新..."** 菜单，打开"Visual Studio **更新**"对话框。
2. 如果有可用的更新，请单击"安装 **"** 按钮。

:::zone-end

## <a name="configure-unity-to-use-visual-studio"></a>配置 Unity 以使用Visual Studio

默认情况下，Unity 应已配置为使用Visual Studio或Visual Studio for Mac脚本编辑器。 可以确认此操作，或者从 Unity 编辑器将外部脚本编辑器Visual Studio特定版本的脚本。

:::zone pivot="windows"

1. 在 Unity 编辑器中，选择"编辑> **首选项"** 菜单。
2. 选择左侧 **的** "外部工具"选项卡。
3. "**外部脚本编辑器**"下拉列表提供了一种方法，用于选择不同安装Visual Studio。 还可以从下拉列表 **中** 单击"浏览..."，添加未列出的版本。

    !["Unity 编辑器"中的"外部工具"首选项菜单Windows](../media/vs/preferences-external-tools.png)

4. 如果已选择 **Browse...** ，请导航到 Visual Studio 安装目录中的 **Common7/IDE** 目录，然后选择 **devenv.exe**。 然后单击"打开 **"。**
5. 在 **External Script Editor** 列表中选择 Visual Studio 后，确认已选中 **Editor Attaching** 复选框。
6. 关闭 **Preferences** 对话框以完成配置过程。

:::zone-end
:::zone pivot="macos"

1. 在 Unity 编辑器中，选择 **"Unity >首选项"** 菜单。
2. 选择左侧 **的** "外部工具"选项卡。
3. "**外部脚本编辑器**"下拉列表提供了一种方法，用于选择不同安装Visual Studio。 还可以从下拉列表 **中** 单击"浏览..."，添加未列出的版本。

    ![macOS 上的 Unity 编辑器中的"外部工具"首选项菜单](../media/vsm/preferences-external-tools.png)

4. 关闭 **Preferences** 对话框以完成配置过程。

:::zone-end

## <a name="next-steps"></a>后续步骤

 若要了解如何在 Visual Studio 中处理和调试 Unity 项目，请访问[使用 Visual Studio Tools for Unity。](using-visual-studio-tools-for-unity.md)
