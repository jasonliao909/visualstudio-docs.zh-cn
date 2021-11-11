---
title: Visual Studio 如何简化源代码管理
titleSuffix: ''
description: 了解如何在 Visual Studio 中使用 Git 和 GitHub 来跟踪代码更改，并在需要时将其还原。
ms.date: 11/08/2021
ms.topic: conceptual
ms.author: tglee
author: TerryGLee
ms.manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: a32ef55b8f14da7931557b533464804672de1b49
ms.sourcegitcommit: 67dc39e93c86ba50eb5ca877b0471fb8ab8475ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2021
ms.locfileid: "132001913"
---
# <a name="how-visual-studio-makes-source-control-easy"></a>Visual Studio 如何简化源代码管理

你是否曾经希望恢复到旧版本的能正常运行的代码？ 你是否将代码副本手动存储在不同位置作为备份？ 通过源代码管理，你可以跟踪一段时间内对代码的更改，以便跟踪进度并还原到特定版本。 通过 Visual Studio 可以轻松使用 Git，这是最广泛使用的现代版本控制系统。

## <a name="a-great-place-to-start-with-git--github"></a>开始使用 Git 和 GitHub 的好地方

GitHub 提供免费且安全的云代码存储，你可以在其中存储代码并从任意位置使用任意设备访问它。 Visual Studio 附带卓越的 Git 和 GitHub 功能，让你可以轻松地使用源代码管理来管理你的代码并与他人协作。 首先使用以下“创建 Git 存储库”对话框将你的代码添加到“Git 和 GitHub”。 为此，请从菜单栏中选择“Git” > “创建 Git 存储库” 。

:::image type="content" source="media/git-source-control-create-repository.png" alt-text="Visual Studio 中“创建 Git 存储库”对话框。":::

还可以使用 GitHub 浏览大量开源存储库并从中学习。 使用 Visual Studio 可以轻松地克隆和浏览现有的 GitHub 存储库，因此这是一个非常好的学习环境。

## <a name="streamlined-and-intuitive-inner-loop-git-experience"></a>精简且直观的内部循环 Git 体验

Visual Studio 提供可发现的直观 Git 功能，旨在最大程度地提高日常工作流（内部循环）的效率。 不再需要离开代码即可提交更改。 这些功能包括顶级 Git 菜单、“Git 更改”窗口和 Git 焦点状态栏。 Git 与 Visual Studio 集成为一个整体体验；例如，解决方案资源管理器和代码编辑器都具有卓越的 Git 集成。

:::image type="content" source="media/git-source-control-inner-loop.png" alt-text="Visual Studio IDE，显示了解决方案资源管理器中的 Git 菜单和“Git 更改”选项卡。":::

## <a name="first-class-repository-management--collaboration"></a>卓越的存储库管理和协作

Visual Studio 包含强大的存储库浏览和协作功能，让你无需使用其他工具。 随时关注你的传入/传出提交、预览分支和比较提交，始终了解你的存储库。 同时，通过管理分支、Squash 合并提交和挑拣提交来管理存储库。

:::image type="content" source="media/git-source-control-repository-management.png" alt-text="Visual Studio IDE，突出显示了解决方案资源管理器中的 Git 菜单和“Git 更改”选项卡。":::

## <a name="interactive--smart-git-functionality"></a>交互式智能 Git 功能

Visual Studio 中的 Git 集成通过提供上下文帮助并提示你执行正确操作来增强信任和信心。 它还包括冲突解决体验，可显示/隐藏字词差异，并在冲突和差异之间导航。

:::image type="content" source="media/git-source-control-interactive-functionality.png" alt-text="Visual Studio IDE，显示了 Git 上下文协助和冲突解决。":::

## <a name="next-steps"></a>后续步骤

若要详细了解如何在 Visual Studio 2019 中使用 Git 和 GitHub，请观看以下 YouTube 视频：[在 Visual studio 中开始使用 Git](https://www.youtube.com/watch?v=GCZ9x3yqkyc&list=PLReL099Y5nRc-zbaFbf0aNcIamBQujOxP)

## <a name="see-also"></a>请参阅

- [Visual Studio 2019 中的 Git 和 GitHub 入门](/learn/modules/visual-studio-github-push/)
- [Visual Studio 2019 中的 Git 新体验](git-with-visual-studio.md?view=vs-2019&preserve-view=true)
- [在 Visual Studio 2019 中并行比较 Git 和团队资源管理器](git-team-explorer-feature-comparison.md?view=vs-2019&preserve-view=true)