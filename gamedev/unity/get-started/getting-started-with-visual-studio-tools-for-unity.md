---
title: 快速入门：安装并配置 Visual Studio Tools for Unity
description: 了解如何连接 Unity 和 Visual Studio 以进行跨平台开发。
ms.date: 11/17/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: quickstart
ms.assetid: 66b5b4eb-13b5-4071-98d2-87fafa4598a8
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
zone_pivot_groups: platform
ms.openlocfilehash: a27ec6f2fa0cd9ffc6eb3e62b7de4b7a2adaee0a
ms.sourcegitcommit: dd66ab447c6f33de525f9429de1f912dd538a6d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2021
ms.locfileid: "132773156"
---
# <a name="quickstart-configure-visual-studio-for-cross-platform-development-with-unity"></a>快速入门：配置 Visual Studio 以使用 Unity 进行跨平台开发

在本快速入门中，你将了解如何安装 Visual Studio Tools for Unity 扩展并对其进行配置，以使用 Unity 开发跨平台游戏和应用。  Visual Studio Tools for Unity 扩展是免费的，并且支持编写和调试 C# 等等。 有关扩展所包含内容的完整列表，请访问 [Tools for Unity 概述](./visual-studio-tools-for-unity.md)。

> [!NOTE]
> 对于 Visual Studio Code 和 Unity，请访问[使用 VS Code 的 Unity 开发文档](https://code.visualstudio.com/docs/other/unity)。

## <a name="prerequisites"></a>先决条件

+ 本指南假定已使用 Unity Hub 程序安装了 Unity。 如果刚开始接触 Unity，请先完成 [Unity Essentials 学习路径](https://learn.unity.com/pathway/unity-essentials)。

## <a name="install-visual-studio-tools-for-unity"></a>安装 Visual Studio Tools for Unity

:::zone pivot="windows"

1. [下载 Visual Studio 安装程序](/visualstudio/install/install-visual-studio)，如已安装，则运行该安装程序。
2. 为所需的 Visual Studio 版本单击“修改”（如已安装）或“安装”（适用于新安装）。
3. 在“工作负载”选项卡上，滚动到“游戏”部分，并选择“使用 Unity 的游戏开发”工作负载。

    ![安装程序中的“使用 Unity 的游戏开发”工作负载框](../media/vs/unity-workload.png)

:::zone-end
:::zone pivot="macos"

Tools for Unity 包含在 Visual Studio for Mac 安装中，无需单独安装步骤。 可以在“Visual Studio for Mac > 扩展 > 游戏开发”菜单中对此进行验证。 Visual Studio for Mac Tools for Unity 应已启用。

![显示 Visual Studio for Mac Tools for Unity 已启用的扩展管理器视图](../media/vsm/unity-workload.png)

:::zone-end

## <a name="check-for-updates"></a>检查更新

建议更新 Visual Studio 和 Visual Studio for Mac，以便获取最新的 bug 修复、功能和 Unity 支持。 这不需要更新 Unity 版本。

:::zone pivot="windows"

1. 单击“帮助”>“检查更新”菜单。

    ![Visual Studio 2019 中的“检查更新”菜单](../media/vs/check-for-updates.png)

2. 如果有可用的更新，Visual Studio 安装程序将显示新版本。 单击“更新”按钮。

:::zone-end
:::zone pivot="macos"

1. 单击“Visual Studio for Mac > 检查更新...”菜单以打开“Visual Studio 更新”对话框。
2. 如果有可用的更新，请单击“安装”按钮。

:::zone-end

## <a name="configure-unity-to-use-visual-studio"></a>配置 Unity 以使用 Visual Studio

默认情况下，Unity 应已配置为使用 Visual Studio 或 Visual Studio for Mac 作为脚本编辑器。 可以确认下是否如此，或者将外部脚本编辑器由 Unity 编辑器更改为特定版本的 Visual Studio。

:::zone pivot="windows"

1. 在 Unity 编辑器中，选择“编辑 > 首选项”菜单。
2. 选择左侧的“外部工具”选项卡。
3. 可通过“外部脚本编辑器”下拉列表选择不同的 Visual Studio 安装方法。 还可以从下拉列表单击“浏览...”以添加未列出的版本。

    ![Windows 上 Unity 编辑器中的“外部工具”首选项菜单](../media/vs/preferences-external-tools.png)

4. 如果已选择 **Browse...** ，请导航到 Visual Studio 安装目录中的 **Common7/IDE** 目录，然后选择 **devenv.exe**。 然后单击“打开”。
5. 在 **External Script Editor** 列表中选择 Visual Studio 后，确认已选中 **Editor Attaching** 复选框。
6. 关闭 **Preferences** 对话框以完成配置过程。

:::zone-end
:::zone pivot="macos"

1. 在 Unity 编辑器中，选择“Unity > 首选项”菜单。
2. 选择左侧的“外部工具”选项卡。
3. 可通过“外部脚本编辑器”下拉列表选择不同的 Visual Studio 安装方法。 还可以从下拉列表单击“浏览...”以添加未列出的版本。

    ![macOS 上 Unity 编辑器中的“外部工具”首选项菜单](../media/vsm/preferences-external-tools.png)

4. 关闭 **Preferences** 对话框以完成配置过程。

:::zone-end

## <a name="next-steps"></a>后续步骤

了解此扩展的[集成和生产力功能，以及如何使用 Visual Studio 调试器进行 Unity 开发](using-visual-studio-tools-for-unity.md)。
