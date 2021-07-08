---
title: 了解解决方案资源管理器工具窗口
description: 了解如何在 Visual Studio 中使用解决方案资源管理器工具窗口创建和管理文件、项目以及解决方案。
ms.date: 06/29/2021
ms.topic: conceptual
f1_keywords:
- vs.addnewitem
helpviewer_keywords:
- solution explorer [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fbbae8b974a7e88abffd9a12eb253dfea6c7165b
ms.sourcegitcommit: 8fb1500acb7e6314fbb6b78eada78ef5d61d39bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2021
ms.locfileid: "113280492"
---
# <a name="how-to-use-solution-explorer"></a>如何使用解决方案资源管理器

可以使用解决方案资源管理器工具窗口来创建解决方案和项目并对其进行管理，以及查看代码并与之交互。 在本文中，我们将详细介绍可帮助执行此类操作的用户界面 (UI) 选项。

> [!NOTE]
> 本主题仅适用于 Windows 上的 Visual Studio。

## <a name="solution-explorer-tool-window"></a>解决方案资源管理器工具窗口

首先，我们了解一下 [Visual Studio IDE](../get-started/visual-studio-ide.md) 中的解决方案资源管理器工具窗口，其中有一个打开的 C# 控制台解决方案，该解决方案包含两个项目。

[![Visual Studio 中的解决方案资源管理器工具窗口。](media/solution-explorer-tool-window.png)](media/solution-explorer-tool-window.png#lightbox)

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

## <a name="solution-explorer-menu-bar"></a>“解决方案资源管理器”菜单栏

若要继续，请深入了解“解决方案资源管理器”菜单栏。

![Visual Studio 中的“解决方案资源管理器”菜单栏。](media/solution-explorer-menu-bar.png)

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

### <a name="solution-explorer-right-click-context-menu"></a>解决方案资源管理器右键单击上下文菜单

在解决方案资源管理器中，可以使用右键单击上下文菜单与若干文件属性进行交互。 有关右键单击上下文菜单选项的详细信息，请参阅[管理项目和解决方案属性](managing-project-and-solution-properties.md)页面。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中有哪些解决方案和项目？](solutions-and-projects-in-visual-studio.md)
- [在 Visual Studio 中自定义窗口布局](customizing-window-layouts-in-visual-studio.md)
