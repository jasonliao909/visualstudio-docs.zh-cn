---
title: 在 Visual Studio 中提取、拉取、推送和同步
titleSuffix: ''
description: 在 Visual Studio 中使用 Git 或 Azure DevOps Visual Studio 提取、拉取、推送和同步。
ms.date: 11/08/2021
ms.topic: how-to
author: TerryGLee
ms.author: tglee
ms.manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: 0e532234bdfd694f36d672247986413983bedd15
ms.sourcegitcommit: 67dc39e93c86ba50eb5ca877b0471fb8ab8475ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2021
ms.locfileid: "132002789"
---
# <a name="fetch-pull-and-sync-in-visual-studio"></a>在 Visual Studio 中提取、拉取和同步

Visual Studio 通过下载（提取和拉取）和上传（推送）操作来使本地分支与远程分支保持同步。

你可以在 Visual Studio 2022 中使用“Git”菜单提取、拉取和同步。

:::image type="content" source="media/vs-2022/git-menu-fetch.png" alt-text="Visual Studio 2022 中的“Git”菜单突出显示了“提取”选项。":::

在前面的屏幕截图中，突出显示了“提取”选项。 “Git”菜单还包括以下附加选项：

- **拉取**
- **Push**
- **同步(拉取然后推送)**

你还可以使用“Git 更改”窗口中的按钮控件来执行这些操作。

:::image type="content" source="media/vs-2022/git-changes-window-options.png" alt-text="Visual Studio 2022 中的“Git 更改”窗口突出显示了“提取”、“拉取”、“推送”和“同步”按钮控件。":::

从左到右，按钮控件包括提取、拉取、推送和同步   。

此外，还有一个表示其他操作的省略号 (...) 按钮控件 。 选择它时，会出现一个上下文菜单。 你可以使用它来微调提取、拉取、推送和同步操作。

:::image type="content" source="media/vs-2022/git-changes-window-ellipsis.png" alt-text="在 Visual Studio 2022 的“Git 更改”窗口中选择省略号按钮控件后显示的上下文菜单。":::

## <a name="fetch"></a>提取

在推送之前必须提取并拉取。 提取操作可检查是否有任何远程条件应纳入到本地更改中。 如果发现有，请先拉取它们以防止任何上游合并冲突。

提取分支时，“Git 更改”窗口在分支下拉箭头下有一个指示器，其中显示了远程分支的未拉取提交数。 该指示器还显示未推送的本地提交数。

该指示器还可作为链接，将你带到“Git 存储库”窗口中该分支的提交历史记录。 历史记录的顶部现在会显示这些传入和传出提交的详细信息。 你还可以在这里决定拉取或推送提交。

## <a name="pull"></a>请求

推送前始终拉取。 第一次拉取时，可以防止上游[合并冲突](git-resolve-conflicts.md)。

## <a name="push"></a>推送

创建提交时，你原本就保存了代码的本地快照。 使用推送将提交推送到 GitHub，在这里你可以将其存储为备份或与他人分享你的代码。

但正如前文所述，请始终先拉取后推送。 如果本地分支落后于远程分支，Visual Studio 不允许推送提交以保护安全。 如果尝试推送，会出现一个对话框，提示你在推送之前拉取。

## <a name="sync"></a>同步

同时使用此操作来拉取和推送。

## <a name="next-steps"></a>后续步骤

若要继续学习，请访问[浏览 Git 存储库](git-browse-repository.md)页。

## <a name="see-also"></a>请参阅

[教程：打开存储库中的项目](../get-started/tutorial-open-project-from-repo.md)
