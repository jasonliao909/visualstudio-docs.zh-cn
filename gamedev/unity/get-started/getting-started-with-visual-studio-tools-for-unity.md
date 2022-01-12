---
title: 快速入门：安装并配置 Visual Studio Tools for Unity
description: 了解如何连接 Unity 和 Visual Studio 以进行跨平台开发。
ms.date: 12/10/2021
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
ms.openlocfilehash: 67e0893ad5fd0329a9542ecec5991f8ae641df02
ms.sourcegitcommit: 2a4744fb312396d36086dd59fd55ab741ae8e106
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/28/2021
ms.locfileid: "135575990"
---
# <a name="quickstart-configure-visual-studio-for-cross-platform-development-with-unity"></a>快速入门：配置 Visual Studio 以使用 Unity 进行跨平台开发

在本快速入门中，你将了解如何安装 Visual Studio Tools for Unity 扩展并对其进行配置，以使用 Unity 开发跨平台游戏和应用。  Visual Studio Tools for Unity 扩展是免费的，并且支持编写和调试 C# 等等。 有关扩展所包含内容的完整列表，请访问 [Tools for Unity 概述](./visual-studio-tools-for-unity.md)。

> [!NOTE]
> 对于 Visual Studio Code 和 Unity，请访问[使用 VS Code 的 Unity 开发文档](https://code.visualstudio.com/docs/other/unity)。

## <a name="install-visual-studio-and-unity"></a>安装 Visual Studio 和 Unity

:::zone pivot="windows"

1. [下载 Visual Studio 安装程序](/visualstudio/install/install-visual-studio.md)，如已安装，则打开它。
2. 如果已安装，请选择 "**修改** () 或 (适用于所需版本的 Visual Studio **安装** 新) 安装的。
3. 选择 " **工作负载** " 选项卡，然后选择 " **包含 Unity 的游戏开发** " 工作负荷。    
4. 如果尚未安装 Unity，请在安装程序的 "可选" 部分中选择 "Unity 中心" 复选框。
5. 选择 " **修改** " 或 " **安装** " 以完成安装。

![安装程序中的 "用 Unity 工作负荷进行游戏开发" 对话框的屏幕截图](../media/vs/unity-workload.png)

Visual Studio 完成安装过程后，就可以安装 Unity 了。

1. 打开在 Visual Studio Tools for Unity 安装过程中安装的 Unity 中心。
1. 在 "Unity 中心" 窗口的左侧，选择 " **安装** " 选项卡。
1. 选择“添加”按钮。
1. 在 "添加 Unity 版本" 窗口中，选择要安装的 Unity 版本。
1. 选择 " **下一步** " 继续安装。
1. 在将 **模块添加到安装** 步骤中，选择 " **完成**"。

>[!NOTE]
>如果已安装 Visual Studio 2022，则可以取消选择 Microsoft Visual Studio Community 2019 选项。

Unity 中心将继续在后台安装 Unity。 完成后，可以通过选择 " **项目** " 选项卡并选择 " **新建** " 按钮来创建新项目。

>[!TIP]
>使用 Unity 编辑器创建项目，而不是 Visual Studio。

:::zone-end
:::zone pivot="macos"

> [!NOTE]
> 本安装指南适用于 Visual Studio for Mac。 如果你正在使用 Visual Studio Code，请[使用 VS Code 文档访问 Unity 开发](https://code.visualstudio.com/docs/other/unity)。

Visual Studio for Mac 适用于 Unity 的工具包含在 Visual Studio for Mac 安装中，无需单独安装步骤。 可以在“Visual Studio for Mac > 扩展 > 游戏开发”菜单中对此进行验证。 Visual Studio for Mac Tools for Unity 应已启用。

![显示已启用 Unity Visual Studio for Mac 工具的 "扩展管理器" 视图的屏幕截图](../media/vsm/unity-workload.png)

:::zone-end

## <a name="configure-unity-to-use-visual-studio"></a>配置 Unity 以使用 Visual Studio

默认情况下，Unity 应已配置为使用 Visual Studio 或 Visual Studio for Mac 作为脚本编辑器。 可以确认下是否如此，或者将外部脚本编辑器由 Unity 编辑器更改为特定版本的 Visual Studio。

:::zone pivot="windows"

1. 在 Unity 编辑器中，选择 " **编辑 > 首选项** " 菜单。
2. 在左侧，选择 " **外部工具** " 选项卡。

    ![Windows 上 Unity 编辑器中的外部工具首选项菜单的屏幕截图](../media/vs/preferences-external-tools.png)

### <a name="install-or-update-the-visual-studio-editor-package"></a>安装或更新 Visual Studio 编辑器包

在 Unity 版本2020及更高版本中，对于使用 Visual Studio 的 Ide，最佳体验需要单独的 Unity 包。 默认情况下，这应该包含在内，但我们将发布对此包的更新，你可以随时将其更新到。

1. 在 Unity 编辑器中，选择 " **Windows > 程序包管理器**" 菜单。
1. 选择 **Visual Studio 编辑器** 包。
1. 如果有新版本可用，请选择 " **更新** " 按钮。

![Windows 上 Unity 编辑器中的 "程序包管理器" 窗口的屏幕截图](../media/vs/unity-package-manager.png)

### <a name="add-a-version-of-visual-studio-that-is-not-listed"></a>添加未列出的 Visual Studio 版本
可以选择未列出并安装在自定义目录中的其他 Visual Studio 版本。

1. 从下拉列表中选择 " **浏览 ...** "。
2. 导航到 Visual Studio 安装目录中的 **Common7/IDE** 目录，然后选择 " **devenv.exe**"。 然后单击“打开”。
3. 对于 Unity 2019 和更低版本，请确认已选中 " **编辑器附加** " 复选框。
4. 关闭 **Preferences** 对话框以完成配置过程。

:::zone-end
:::zone pivot="macos"

1. 在 Unity 编辑器中，选择 " **unity > 首选项** " 菜单。
2. 在左侧，选择 " **外部工具** " 选项卡。
3. 使用 "**外部脚本编辑器**" 下拉列表提供一种方法来选择不同的 Visual Studio for Mac 安装。

    ![MacOS 上 Unity 编辑器中的外部工具首选项菜单的屏幕截图](../media/vsm/preferences-external-tools.png)

4. 关闭 **Preferences** 对话框以完成配置过程。

:::zone-end

## <a name="check-for-updates"></a>检查更新

建议更新 Visual Studio 和 Visual Studio for Mac，以便获取最新的 bug 修复、功能和 Unity 支持。 这不需要更新 Unity 版本。

:::zone pivot="windows"

1. 单击“帮助”>“检查更新”菜单。

    ![Visual Studio 2019 中 "检查更新" 菜单的屏幕截图](../media/vs/check-for-updates.png)    

2. 如果有可用的更新，Visual Studio 安装程序将显示新版本。 单击“更新”按钮。

:::zone-end
:::zone pivot="macos"

1. 单击“Visual Studio for Mac > 检查更新...”菜单以打开“Visual Studio 更新”对话框。
2. 如果有可用的更新，请单击“安装”按钮。

:::zone-end

## <a name="next-steps"></a>后续步骤

了解此扩展的[集成和生产力功能，以及如何使用 Visual Studio 调试器进行 Unity 开发](using-visual-studio-tools-for-unity.md)。
