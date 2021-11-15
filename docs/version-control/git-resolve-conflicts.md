---
title: 在 Visual Studio 中解决合并冲突
titleSuffix: ''
description: 在 Visual Studio 中了解、防止和解决合并冲突。
ms.date: 11/08/2021
ms.topic: how-to
author: Taysser-Gherfal
ms.author: tglee
ms.manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: e6de198dc0e29fd2a44cc6a50aece22f3d9b28d8
ms.sourcegitcommit: 5f60dd61e7f281db7892118dbed6387c4903701f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2021
ms.locfileid: "132079598"
---
# <a name="resolve-merge-conflicts-in-visual-studio"></a>在 Visual Studio 中解决合并冲突

将一个分支合并到另一个分支时，一个分支中提交的文件更改可能会与另一个分支中的更改冲突。 Git 尝试使用存储库中的历史记录来确定合并文件的效果，从而尝试解决这些更改。 如果不清楚如何合并更改，Git 会暂停合并，然后告知哪些文件发生冲突。

## <a name="understand-merge-conflicts"></a>了解合并冲突

下图通过最简单的示例介绍了 Git 中的更改如何发生冲突。 主分支和 bug 修复分支都对相同的源代码行进行更新。

:::image type="content" source="media/vs-2022/git-conflicts-understand-1.png" alt-text="显示合并冲突的关系图。":::

如果尝试将 bug 修复分支合并到主分支中，Git 无法确定合并版本中要使用哪些更改。 你可能想要保留主分支、bug 修复分支或两者的某种组合中的更改。 使用主分支上的合并提交解决此冲突，该合并提交可协调两个分支之间的冲突更改。

:::image type="content" source="media/vs-2022/git-conflicts-understand-2.png" alt-text="显示合并提交如何解决合并冲突的关系图。":::

最常见的合并冲突情况是将更新从远程分支拉取到本地分支，例如从源/bug 修复分支拉取到本地 bug 修复分支。 以相同方式解决这些冲突 - 在本地分支上创建用于协调更改的合并提交并完成合并。

## <a name="prevent-merge-conflicts"></a>防止合并冲突

在大多数情况下，Git 非常擅长自动合并文件更改，前提是各提交之间的文件内容没有大幅改动。 如果你的分支远远落后于主分支，请考虑在开立拉取请求之前变基分支。 变基分支将合并到主分支中，而不会发生冲突。

## <a name="resolve-merge-conflicts"></a>解决合并冲突

- 如果你在与其他人协作处理同一分支，那么你在推送你的更改时也可能会遇到合并冲突。

    :::image type="content" source="media/vs-2022/git-conflicts-push-link.png" alt-text="推送后合并冲突的屏幕截图。":::

- 推送更改时，Visual Studio 会检测你一直在处理的本地分支是否落后于其远程跟踪分支，并为你提供多个选项进行选择。

    :::image type="content" source="media/vs-2022/git-conflicts-pull-push-ui.png" alt-text="本地分支落后于远程分支时可用选项的屏幕截图。":::

    > [!NOTE]
    > 如果远程存储库支持强制推送，你可以通过“Git”>“设置”启用强制推送。

- 让我们选择“拉取然后推送”以添加引入远程存储库的更改。 如果在拉取更改或尝试合并两个分支时存在任何合并冲突，Visual Studio 会通过“Git 更改”窗口、“Git 存储库”窗口以及任何存在冲突的文档通知我们。

    :::image type="content" source="media/vs-2022/git-conflicts-notification-ui.png" alt-text="合并冲突通知的屏幕截图。" lightbox="media/vs-2022/git-conflicts-notification-ui.png":::

- “Git 更改”窗口在“未合并的更改”下显示存在冲突的文档列表。 若要开始解决冲突，可双击要解决的文档；如果在编辑器中打开了存在冲突的文档，可单击“打开合并编辑器”。

    :::image type="content" source="media/vs-2022/git-conflicts-status-ui.png" alt-text="“Git 更改”窗口中的合并冲突状态的屏幕截图。" lightbox="media/vs-2022/git-conflicts-status-ui.png":::

- 打开合并编辑器后，可使用以下任一方法开始解决冲突：
    1. 逐行查看冲突，并通过勾选复选框选择保留左侧还是右侧更改。
    1. 保留或忽略所有存在冲突的更改。
    1. 在“结果”窗口中手动编辑代码。

    :::image type="content" source="media/vs-2022/git-conflicts-resolve-conflict.png" alt-text="显示如何在 Visual Studio 2022 中解决合并冲突的屏幕截图。" lightbox="media/vs-2022/git-conflicts-resolve-conflict.png":::

    > [!TIP]
    > 如果不喜欢合并编辑器的默认布局，可随时使用齿轮下拉菜单进行更改。
    > :::image type="content" source="media/vs-2022/git-conflicts-layout-options.png" alt-text="合并编辑器布局选项的屏幕截图。":::
    >
    >例如，以下屏幕截图显示了垂直视图的呈现效果：
    >
    > :::image type="content" source="media/vs-2022/git-conflicts-vertical-view.png" alt-text="合并编辑器用户界面中垂直视图的屏幕截图。" lightbox="media/vs-2022/git-conflicts-vertical-view.png":::

- 解决合并冲突后，选择“接受合并”。 针对所有冲突文件重复此操作。

    :::image type="content" source="media/vs-2022/git-conflicts-accept-merge.png" alt-text="Visual Studio 2022 中的“接受合并”操作的屏幕截图。":::

- 使用“Git 更改”窗口创建合并提交并解决冲突。

    :::image type="content" source="media/vs-2022/git-conflicts-merge-commit.png" alt-text="显示如何使用“Git 更改”窗口创建合并提交的屏幕截图。":::

    > [!NOTE]
    > 如果需要保留对文档的所有更改，可在“未合并的更改”部分下右键单击该文档，然后选择“保留当前项(本地)”，无需打开合并编辑器 。
    >
    > :::image type="content" source="media/vs-2022/git-conflicts-keep-changes.png" alt-text="“保留当前项和提取传入项”菜单选项的屏幕截图。":::

## <a name="next-steps"></a>后续步骤

若要继续学习，请使用以下链接详细了解合并和合并冲突 [Git 合并和解决冲突](https://git-scm.com/docs/git-merge)。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 Git 体验](../ide/git-with-visual-studio.md)