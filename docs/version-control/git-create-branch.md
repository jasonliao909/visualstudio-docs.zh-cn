---
title: 在 Visual Studio 中创建分支
titleSuffix: ''
description: 在 Visual Studio 中使用 Git 或 Azure DevOps 创建分支。
ms.date: 11/10/2021
ms.topic: how-to
author: TerryGLee
ms.author: tglee
ms.manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: 9f6e72e1254f251114b1798d97e2937ddd41aab0
ms.sourcegitcommit: dc12d3d0ca2ec3601cb9de7c22e61ecf22c7c514
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2021
ms.locfileid: "132263997"
---
# <a name="create-a-branch-in-visual-studio"></a>在 Visual Studio 中创建分支

在 Visual Studio 中创建一个新分支很简单，只需基于现有分支即可创建。

操作方法如下。

1. 开始操作之前，请确保已打开先前[创建的](git-create-repository.md)或[的](git-clone-repository.md)存储库。

1. 从“Git”菜单中，选择“新建分支” 。

    :::image type="content" source="media/vs-2022/git-menu-new-branch.png" alt-text="“Git”菜单中“新建分支”选项的屏幕截图。":::

1. 在“创建新分支”对话框中，输入分支名称。

    :::image type="content" source="media/vs-2022/git-create-new-branch-dialog.png" alt-text="“创建新分支”对话框的屏幕截图。":::

1. 在“基于”部分中，使用下拉列表来选择是要基于现有的本地分支还是远程分支创建新分支。

1. 默认启用的“签出分支”复选框会自动切换到新创建的分支。 如果希望保留在当前分支中，请切换此选项。

就是这样；您已创建一个新分支。

> [!TIP]
> 此操作的等效命令是 `git checkout -b <new-branch> <existing-branch>`。

## <a name="next-steps"></a>后续步骤

若要继续学习，请访问[创建提交](git-make-commit.md)页面。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 Git 体验](git-with-visual-studio.md)
- [Visual Studio 和 GitHub：更好地协同工作](https://visualstudio.microsoft.com/vs/github/)