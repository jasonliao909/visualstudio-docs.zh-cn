---
title: 在 Visual Studio 中浏览存储库
titleSuffix: ''
description: 在 Visual Studio 中使用“Git 存储库”窗口浏览任何 Git 存储库。
ms.date: 11/05/2021
ms.topic: how-to
author: Taysser-Gherfal
ms.author: tglee
ms.manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: ad071fefa6d6069f35401ca777cdad07eb74ff36
ms.sourcegitcommit: 67dc39e93c86ba50eb5ca877b0471fb8ab8475ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2021
ms.locfileid: "132002825"
---
# <a name="browse-git-repositories-in-visual-studio"></a>在 Visual Studio 中浏览 Git 存储库

“Git 更改”窗口提供了一种无缝方式，可以在编码的同时与 Git 交互，而无需离开代码；但是，有时将焦点放在 Git 存储库上会更有意义。 例如，你可能需要了解团队一直在处理什么，或者比较两个提交以调查 bug。

## <a name="browse-local-and-remote-branches"></a>浏览本地和远程分支

若要开始操作，请通过单击“视图”菜单上的“Git 存储库”打开“Git 存储库”窗口。 你还可通过单击“Git 更改”窗口和状态栏中的“传出/传入”链接来访问“Git 存储库”窗口。

:::image type="content" source="media/vs-2022/git-repository-browse-ui.png" alt-text="屏幕截图显示“Git 存储库”窗口的剖析":::

“Git 存储库”窗口包含 3 个主要部分，如前面的屏幕截图所示：
1. **分支：** Git 通过分支使用户能够执行多任务并试验代码。 如果同时处理多个功能，或者要探索想法而不影响工作代码，则分支可能会非常有用。
1. **Git 图：** “Git 图”部分能够可视化分支的状态。 它包含三个不同的部分：传入、传出和本地历史记录。 “传入”部分显示团队提供的传入提交，“传出”部分显示尚未推送的本地提交，本地历史记录显示本地存储库跟踪的其余提交。
1. **提交详细信息：** 单击“Git 图”部分中的任何提交会打开提交详细信息 UI，其中显示了提交的详细信息。 单击提交详细信息可以显示差异，从而检查这些提交引入的更改。 例如，在上一个屏幕截图中可以看到我们正在查看由一个提交引入 Files.csproj 文件的更改

无需切换分支即可浏览任何本地或远程分支，当你找到一个你想关注的提交，只需单击“在新选项卡中打开”按钮，即可在另一个选项卡中打开提交，或在另一个屏幕中将其最大化，如此处所示。

:::image type="content" source="media/vs-2022/git-repository-open-new-tab.png" alt-text="在新选项卡中打开的屏幕截图":::

:::image type="content" source="media/vs-2022/git-repository-details-tab.png" alt-text="“提交详细信息”选项卡的屏幕截图":::

> [!TIP]
> 若要全屏显示提交，请分离提交选项卡，然后使用最大化按钮将提交窗口最大化。 你还可以单击“差异配置齿轮”来选择喜欢的差异配置。
>:::image type="content" source="media/vs-2022/git-repository-commit-details-full-screen.png" alt-text="包含差异配置的全屏提交详细信息的屏幕截图":::

## <a name="compare-commits"></a>比较提交

若要比较分支中的任意两个提交，请使用键盘上的 Ctrl 键选择要比较的两个提交。 然后右键单击其中一个，选择“比较提交”选项。

:::image type="content" source="media/vs-2022/git-repository-compare-commits-option.png" alt-text="如何比较两个提交的屏幕截图":::

:::image type="content" source="media/vs-2022/git-repository-compare-commits-ui.png" alt-text="比较提交 UI 的屏幕截图":::

> [!TIP]
>与提交详细信息类似，你可以使用“在新选项卡中打开”按钮在另一选项卡中打开比较提交 UI，或在另一屏幕中将其最大化。

## <a name="next-steps"></a>后续步骤

若要继续学习，请访问[在 Visual Studio 中管理 Git 存储库](git-manage-repository.md)页。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 Git 体验](../ide/git-with-visual-studio.md)