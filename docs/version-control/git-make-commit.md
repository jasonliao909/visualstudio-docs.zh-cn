---
title: 在 Visual Studio 中进行提交
titleSuffix: ''
description: 在 Visual Studio 中使用 Git 或 Azure DevOps 进行提交。
ms.date: 11/10/2021
ms.topic: how-to
author: TerryGLee
ms.author: tglee
ms.manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: 85c284f33799239e0409a370d6fa1c43e59dbb5b
ms.sourcegitcommit: dc12d3d0ca2ec3601cb9de7c22e61ecf22c7c514
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2021
ms.locfileid: "132264209"
---
# <a name="make-a-commit-in-visual-studio"></a>在 Visual Studio 中进行提交

任何 Git 工作流的核心部分都是修改文件并提交这些文件中的更改。

当你操作时，Git 会跟踪存储库中的文件更改，并将存储库中的文件分为三类。 这些更改等效于在命令行中输入 `git status` 命令时看到的内容：

- **未修改的文件**：自上次提交以来，这些文件未更改。
- **已修改的文件**：自上次提交以来，这些文件已更改，但尚未被暂存以用于下一次提交。
- **已暂存的文件**：这些文件已更改并将添加到下一次提交中。

当你执行操作时，Visual Studio 会在“Git 更改”窗口的“更改”部分中跟踪对项目的文件更改 。

:::image type="content" source="media/vs-2022/git-changes-window.png" alt-text="Visual Studio 2022 中“Git 更改”窗口。":::

若要在就绪时暂存更改，请选择要暂存的每个文件上的“+”（加号）按钮，或右键单击文件，然后选择“暂存” 。 还可以使用“更改”部分顶部的暂存全部 +（加号）按钮，一键暂存所有已修改的文件 。

暂存更改时，Visual Studio 将创建“已暂存的更改”部分。 只有“已暂存的更改”部分的更改会添加到下一次提交中，可以通过选择“提交暂存内容”来执行此操作 。 此操作的等效命令是 `git commit -m "Your commit message"`。

:::image type="content" source="media/vs-2022/git-commit-message.png" alt-text="Visual Studio 2022 中的“Git 提交”对话框。":::

还可单击“–”（减号）按钮来取消暂存更改。 此操作的等效命令是 `git reset <file_path>`（用于取消暂存一个文件）或 `git reset <directory_path>`（用于取消暂存目录中的所有文件）。

也可以通过跳过暂存区域来选择不暂存已修改的文件。 在这种情况下，Visual Studio 允许直接提交更改，而无需暂存更改。 只需输入提交消息，然后选择“全部提交”。 此操作的等效命令是 `git commit -a`。

还可通过 Visual Studio 的“全部提交并推送”和“全部提交并同步”快捷方式，轻松地一键提交和同步 。 双击“更改”和“已暂存的更改”部分中的任何文件时，可以看到与该文件的未修改版本的逐行比较 。

:::image type="content" source="media/vs-2022/git-file-version-compare.png" alt-text="Visual Studio 2022 中文件版本的逐行比较。":::

双击“提交”时，Visual Studio 会在单独的工具窗口中打开其详细信息。 在此处，你可以还原提交、重置提交、修改提交消息，或在提交上创建标记。 在提交中单击已更改的文件时，Visual Studio 将打开该提交及其父级的并排差异视图。

:::image type="content" source="media/vs-2022/git-branch-commit-details.png" alt-text="Visual Studio 2022 中的“提交详细信息”对话框。":::

## <a name="next-steps"></a>后续步骤

若要继续学习，请访问[推送到远程](git-push-remote.md)页面。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 Git 体验](git-with-visual-studio.md)
- [Visual Studio 和 GitHub：更好地协同工作](https://visualstudio.microsoft.com/vs/github/)
