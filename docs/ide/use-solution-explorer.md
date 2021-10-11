---
title: 了解解决方案资源管理器
description: 了解如何在 Visual Studio 中使用解决方案资源管理器工具窗口创建和管理文件、项目以及解决方案。
ms.date: 09/23/2021
ms.topic: conceptual
ms.custom: contperf-fy22q1
f1_keywords:
- vs.addnewitem
helpviewer_keywords:
- solution explorer [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 3daeaa66024db2b3053dd81b205e48b0e215e310
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128429335"
---
# <a name="learn-about-solution-explorer"></a>了解解决方案资源管理器

可以使用解决方案资源管理器工具窗口来创建解决方案和项目并对其进行管理，以及查看代码并与之交互。 在本文中，我们将详细介绍可帮助执行此类操作的用户界面 (UI) 选项。

> [!NOTE]
> 本主题仅适用于 Windows 上的 Visual Studio。

## <a name="tool-window"></a>工具窗口

首先，我们了解一下 [Visual Studio IDE](../get-started/visual-studio-ide.md) 中的解决方案资源管理器工具窗口，其中有一个打开的 C# 控制台解决方案，该解决方案包含两个项目。

[![Visual Studio 中的解决方案资源管理器工具窗口的带批注屏幕截图。](media/solution-explorer-tool-window.png)](media/solution-explorer-tool-window.png#lightbox)

工具窗口包含以下 UI（用户界面）元素：

- 菜单栏 - 用于控制文件显示方式
- 搜索栏 - 用于搜索特定文件和文件类型
- 主窗口 - 用于查看和管理文件、项目以及解决方案
- 解决方案节点 - 用于管理解决方案
- 项目节点 - 用于管理项目
- 依赖项节点 - 用于管理解决方案和项目依赖项
- 程序节点 - 用于查看、编辑和管理程序或应用程序（应用）
- [“Git 更改”选项卡](../version-control/git-with-visual-studio.md?view=vs-2019&preserve-view=true#git-changes-window) - 可用于使用 Visual Studio 中的 Git 和 GitHub 与团队协作处理项目

> [!TIP]
> 如果没有看到解决方案资源管理器工具窗口，可以从 Visual Studio 菜单栏中使用“查看” > “解决方案资源管理器”或按 Ctrl+Alt+L 将其打开    。

## <a name="menu-bar"></a>菜单栏

若要继续，请深入了解“解决方案资源管理器”菜单栏。

![Visual Studio 中的解决方案资源管理器菜单栏的带批注屏幕截图。](media/solution-explorer-menu-bar.png)

菜单栏包含以下 UI 元素，从左到右依次是：

- “返回”按钮，用于在搜索结果之间切换
- “转发”按钮，用于在搜索结果之间切换
- “主页”按钮，用于返回默认视图
- “切换”按钮，用于在解决方案和可用视图之间切换
- “挂起的更改筛选器”按钮和下拉菜单，用于查看打开的文件或具有挂起的更改的文件
- “与活动文档同步”按钮，用于在代码编辑器中查找文件
- “刷新”按钮，仅在选择依赖项（例如函数或包）时出现
- “全部折叠”按钮，用于折叠主窗口中的文件视图
- “显示所有文件”按钮，用于查看所有文件，包括[已卸载的项目](filtered-solutions.md#toggle-unloaded-project-visibility)
- “属性”按钮，用于查看和更改特定文件以及组件的设置
- “预览选定项”按钮，用于在代码编辑器中查看选定的文件或组件

## <a name="context-menu"></a>上下文菜单

在解决方案资源管理器中，可使用上下文菜单与很多选项进行交互。 C# 应用的下列屏幕截图显示了上下文菜单选项，会在你右键单击“解决方案”节点时出现。

:::image type="content" source="media/solution-explorer-context-menu.png" alt-text="解决方案资源管理器中的右键单击上下文菜单屏幕截图。":::

“解决方案”节点的上下文菜单中显示的内容还取决于你的项目类型、编程语言或平台。 以下屏幕截图突出显示了 C# 应用的下列额外选项：“项目依赖项”、“项目生成顺序”、“设置启动项目”和“Git”弹出菜单   。 通常，在向解决方案添加其他项目，然后将其添加到存储库中时，会显示这些额外选项。

:::image type="content" source="media/solution-explorer-context-menu-extra-items.png" alt-text="解决方案资源管理器中的右键单击上下文菜单屏幕截图，其中有额外选项。":::

## <a name="add-menu"></a>添加菜单

在解决方案资源管理器上下文菜单中，最有用的选项之一是“添加”弹出菜单。 从这里，可向解决方案[添加其他项目](../get-started/csharp/tutorial-console-part-2.md#add-another-project)。 还可向项目[添加项](reference/add-new-item-command.md)等。

:::image type="content" source="media/solution-explorer-context-menu-add-flyout.png" alt-text="解决方案资源管理器中右键单击上下文菜单中的“添加”弹出菜单屏幕截图。":::

可通过“解决方案”节点、“项目”节点或“依赖项”节点查看“添加”弹出菜单   。 选项因你使用的节点而异。

如需在教程中了解如何使用解决方案资源管理器中的上下文菜单向项目添加项，请参阅[项目和解决方案简介](../get-started/tutorial-projects-solutions.md#add-an-item-to-the-project)页面。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中有哪些解决方案和项目？](solutions-and-projects-in-visual-studio.md)
- [在 Visual Studio 中自定义窗口布局](customizing-window-layouts-in-visual-studio.md)
