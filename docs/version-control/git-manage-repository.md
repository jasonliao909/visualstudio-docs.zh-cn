---
title: 在 Visual Studio 中管理存储库
titleSuffix: ''
description: 在 Visual Studio 中使用“Git 存储库”窗口管理任何 Git 存储库。
ms.date: 11/10/2021
ms.topic: how-to
author: Taysser-Gherfal
ms.author: tglee
ms.manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: 2c1679fa7558eb7e241fe62b1df30e33d5ba6ef5
ms.sourcegitcommit: dc12d3d0ca2ec3601cb9de7c22e61ecf22c7c514
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2021
ms.locfileid: "132264017"
---
# <a name="manage-git-repositories-in-visual-studio"></a>在 Visual Studio 中管理 Git 存储库

“Git 存储库”窗口提供了一个全屏 Git 体验，重点是帮助你管理 Git 存储库并随时掌握团队的最新动态。 例如，你可能需要重置、还原、挑拣提交或仅清理提交历史记录。 “Git 存储库”窗口也是可视化和管理分支的理想位置。

## <a name="change-the-last-commit-amend"></a>更改上次提交（修正）

Git 将更新上次提交称为修正，这是一个非常常见的用例。 有时你只需更新提交消息，否则可能需要包含最新的更改。

你可以使用以下命令在命令行中修正提交：

```bash
git commit --amend
```

“Git 存储库”窗口可让你轻松更新提交消息。 只需双击上次提交打开上次提交的提交详细信息，然后单击提交消息旁边的“编辑”选项即可。

:::image type="content" source="media/vs-2022/git-repository-edit-commit.png" alt-text="编辑提交消息的屏幕截图。" lightbox="media/vs-2022/git-repository-edit-commit.png":::

完成提交消息的编辑后，单击“修正”。

:::image type="content" source="media/vs-2022/git-repository-amend-commit.png" alt-text="单击“修正”保存已编辑消息的屏幕截图。" lightbox="media/vs-2022/git-repository-amend-commit.png":::

如果需要包含对上次提交的代码更改，可以通过选中“修正”复选框并提交所做的更改，使用“Git 更改”窗口执行此操作。

:::image type="content" source="media/vs-2022/git-changes-amend-commit.png" alt-text="使用“Git 更改”窗口修正代码更改的屏幕截图。" lightbox="media/vs-2022/git-changes-amend-commit.png":::

> [!TIP]
> 请随意使用以下链接详细了解修正和重写历史记录：[Git 工具 - 重写历史记录](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)

## <a name="merge-commits-squash"></a>合并提交 (Squash)

为了合并一系列提交，Git 提供了一个选项来将多个提交 squash 到单个提交中。 当你频繁创建提交并最终获得数量繁多的提交，而你想要在推送到远程存储库之前清理这些提交时，这会很有帮助。

你可以使用以下命令在命令行中 squash 两项提交：

```bash
git rebase -i HEAD~2
```

然后将挑选更新为 squash、保存和更新提交消息，如下所示 ：

:::image type="content" source="media/vs-2022/git-repository-squash-cmd.png" alt-text="将挑选更新为 squash 的屏幕截图。" lightbox="media/vs-2022/git-repository-squash-cmd.png":::

若要在 Visual Studio 中合并提交，请使用 Ctrl 键，然后选择要合并的多个提交。 然后单击右键并选择“Squash 提交”。 Visual Studio 会自动组合你的提交消息，但有时最好是提供更新的消息。 查看并更新提交消息后，单击“Squash”按钮。

:::image type="content" source="media/vs-2022/git-repository-squash-visual-studio.png" alt-text="Visual Studio 中 squash 提交的屏幕截图。" lightbox="media/vs-2022/git-repository-squash-visual-studio.png":::

> [!TIP]
> 请随时使用以下链接详细了解 Squash 和重写历史记录：[Git 工具 - 重写历史记录](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)

## <a name="merge-and-rebase-branches"></a>合并和变基分支

如果你使用 Git 分支来处理不同的功能，则在某个时候，你需要包含引入到其他分支的更新。 当你仍在处理功能分支，或者已处理功能分支并且需要通过将其添加到另一个分支来保留更改时，可能会发生这种情况。 在 Git 中，可以通过合并或变基分支来实现此目的。

若要将主分支合并到命令行中的 New_Feature 分支，请使用以下命令：

```bash
git checkout New_Feature
git merge main
```

若要在 Visual Studio 中执行相同操作，请在分支列表中双击 New_Feature 分支以将其签出。 然后右键单击主分支并选择“将‘主分支’合并到‘New_Feature 分支’”

:::image type="content" source="media/vs-2022/git-repository-merge-ui.png" alt-text="Visual Studio 中合并分支的屏幕截图。":::

若要在命令行中将主分支变基到 New_Feature 分支，请使用以下命令：

```bash
git checkout New_Feature
git rebase main
```

若要在 Visual Studio 中执行相同操作，请在分支列表中双击 New_Feature 分支以将其签出。 然后右键单击主分支并选择“将‘New_Feature 分支’变基到‘主分支’”

:::image type="content" source="media/vs-2022/git-repository-rebase-ui.png" alt-text="Visual Studio 中变基分支的屏幕截图。":::

> [!TIP]
> 请随时使用以下链接从总体上详细了解合并、变基和分支：[Git 分支](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)

## <a name="copy-commits-cherry-pick"></a>复制提交（挑拣）

使用挑拣将提交从一个分支复制到另一个分支。 与合并或变基不同，挑拣仅引入所选提交中的更改，而不是分支中的所有更改。 挑拣非常适合解决以下常见问题：

- 意外提交错误的分支。 将更改挑拣到正确的分支，然后将原始分支重置为以前的提交。
- 拉取在功能分支中进行的一组提交，以便更快地将它们合并回主分支。
- 在不变基分支的情况下，从主分支植入特定提交。

若要使用命令行将更改从提交复制到当前分支，请使用以下命令：

```bash
git cherry-pick 7599e530
```

若要在 Visual Studio 中执行相同操作，请单击选中要从中挑拣提交的分支以预览该分支。 然后右键单击目标提交，选择“挑拣”。

:::image type="content" source="media/vs-2022/git-repository-cherry-pick-ui.png" alt-text="Visual Studio 中挑拣的屏幕截图。" lightbox="media/vs-2022/git-repository-cherry-pick-ui.png":::

操作完成后，Visual Studio 将显示一条成功消息，并且“传出”部分会显示挑拣的提交。

> [!TIP]
> 请随时使用以下链接详细了解挑拣提交：[Git 挑拣](https://git-scm.com/docs/git-cherry-pick)

## <a name="revert-changes"></a>还原更改

使用还原可撤消推送到共享分支的提交中所做的更改。 还原命令会创建一个新的提交，用于撤消对上一个提交所做的更改。 还原不会重写存储库历史记录，因此在与他人协作时可以安全使用。

若要使用命令行还原在提交中所做的更改，请使用以下命令：

```bash
git revert 53333305
git commit
```

这些命令将撤消提交 53333305 中所做的更改，并在该分支上创建新的提交。 commit_id 的原始提交仍在 Git 历史记录中。 若要在 Visual Studio 中执行相同操作，请右键单击要还原的提交，然后从上下文菜单中选择“还原”。 确认操作并完成该操作后，Visual Studio 将显示一条成功消息，并且“传出”部分会显示新的提交。

:::image type="content" source="media/vs-2022/git-repository-revert-ui.png" alt-text="Visual Studio 中的还原的屏幕截图。" lightbox="media/vs-2022/git-repository-revert-ui.png":::

单击新提交，确认它撤消了对已还原提交的更改。

:::image type="content" source="media/vs-2022/git-repository-revert-confirmation.png" alt-text="确认还原操作的屏幕截图。" lightbox="media/vs-2022/git-repository-revert-confirmation.png":::

> [!TIP]
> 请随意使用以下链接详细了解还原更改：[Git 还原](https://git-scm.com/docs/git-revert)

## <a name="reset-a-branch-to-a-previous-state"></a>将分支重置为以前的状态

使用重置将本地存储库中的分支移回上一个提交的内容。 这只会丢弃在提交重置分支之后的所有更改。
> [!WARNING]
> 请勿在与其他人共享的分支上使用重置。 请改用还原。

若要使用命令行将分支重置为先前的状态，请使用以下命令：

```bash
git reset --hard 53333305
```

命令的 --hard 部分通知 Git 将文件重置为先前提交的状态，并放弃所有暂存的更改。 若要在 Visual Studio 中执行相同操作，请右键单击要重置分支的提交，然后从上下文菜单中选择“重置”>“删除更改(--hard)”。

:::image type="content" source="media/vs-2022/git-repository-reset-ui.png" alt-text="在 Visual Studio 中重置分支。" lightbox="media/vs-2022/git-repository-reset-ui.png":::

> [!TIP]
> 请随意使用以下链接详细了解重置分支：[Git 重置](https://git-scm.com/docs/git-reset)

## <a name="next-steps"></a>后续步骤

若要继续学习，请访问[在 Visual Studio 中解决合并冲突](git-resolve-conflicts.md)页面。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 Git 体验](../ide/git-with-visual-studio.md)
- [Visual Studio 和 GitHub：更好地协同工作](https://visualstudio.microsoft.com/vs/github/)