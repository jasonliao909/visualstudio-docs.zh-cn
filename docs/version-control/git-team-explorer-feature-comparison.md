---
title: Visual Studio 2019 中 Git 和团队资源管理器的并行比较
titleSuffix: ''
description: 比较和对比如何使用 Visual Studio 中的新 Git 体验与团队资源管理器来进行源代码管理。
ms.date: 11/08/2021
ms.topic: how-to
author: Taysser-Gherfal
ms.author: tglee
ms.manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
monikerRange: <=vs-2019
ms.openlocfilehash: 0869ea999132694d06871aa2b7c39cea37463d19
ms.sourcegitcommit: dc12d3d0ca2ec3601cb9de7c22e61ecf22c7c514
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2021
ms.locfileid: "132264166"
---
# <a name="side-by-side-comparison-of-git-and-team-explorer"></a>Git 和团队资源管理器的并行比较

我们在 Visual Studio 2019 [版本 16.8](/visualstudio/releases/2019/release-notes/) 中推出了新 Git 体验的第一个版本。 这种新体验提供包含常见 Git 任务的简单“Git 更改”窗口，可帮助减少上下文切换。 它还包括一个屏幕范围的“Git 存储库”窗口，用于进行更高级的 Git 操作，例如分支管理和存储库浏览。

如果你一直在使用团队资源管理器，下面的分步指南介绍了如何使用新的 Git 体验。

> [!NOTE]
> 下一节包含调整了大小以适应表中各列的屏幕截图。 单击每个屏幕截图以查看其放大版。 （如果使用触屏设备，请点击每个屏幕截图以查看其放大版。）

## <a name="get-started"></a>入门

|         |Team Explorer  |新 Git 体验 |
|---------|---------|---------|
|**克隆存储库** | :::image type="content" source="media/clone-repo-team-explorer-sml.png" alt-text="Visual Studio 2019 中团队资源管理器“连接”窗口的屏幕截图，其中包含“克隆存储库”过程覆盖。" lightbox="media/clone-repo-team-explorer-lrg.png":::  </p>1.打开“连接”页面。 <br> 2.展开“管理连接”。 <br> 3.选择“连接到项目”。 | :::image type="content" source="media/clone-repo-new-git-sml.png" alt-text="Visual Studio 2019 中“Git”菜单的屏幕截图，其中包含“克隆存储库”过程覆盖。" lightbox="media/clone-repo-new-git-lrg.png":::  </p> 1.打开“Git”菜单。 <br>2.选择“克隆存储库”。 <br><br> |
|切换存储库  | :::image type="content" source="media/switch-repos-team-explorer-sml.png" alt-text="Visual Studio 2019 中团队资源管理器“连接”窗口的屏幕截图，其中包含“切换存储库”过程覆盖。" lightbox="media/switch-repos-team-explorer-lrg.png":::  </p>1.打开“连接”页面。 <br>2.从“本地存储库”列表中选择一个存储库。 | :::image type="content" source="media/switch-repos-new-git-sml.png" alt-text="Visual Studio 2019 中“本地存储库”菜单项的屏幕截图，其中包含“克隆存储库”过程覆盖。" lightbox="media/switch-repos-new-git-lrg.png"::: </p> 1.打开“Git”菜单。 <br>2.从“本地存储库”列表中选择一个存储库。  |
|打开解决方案  |  :::image type="content" source="media/open-solution-team-explorer-sml.png" alt-text="Visual Studio 2019 中团队资源管理器“主页”窗口的屏幕截图，其中包含“打开解决方案”过程覆盖。" lightbox="media/open-solution-team-explorer-lrg.png":::</p>1.打开团队资源管理器中的“主页”页面。  <br>2.从解决方案列表中选择一个解决方案。  |  :::image type="content" source="media/open-solution-new-git-sml.png" alt-text="Visual Studio 2019 中解决方案资源管理器的屏幕截图，其中包含“打开解决方案”过程覆盖。" lightbox="media/open-solution-new-git-lrg.png":::</p>1.打开解决方案资源管理器中的“切换视图”页。  <br>2.从解决方案列表中选择一个解决方案。  |
|向源代码管理添加解决方案，并创建新存储库  | :::image type="content" source="media/source-control-team-explorer-sml.png" alt-text="Visual Studio 2019 中团队资源管理器选项的屏幕截图拼贴画，其中显示了“添加到源代码管理 - 创建存储库”过程覆盖。" lightbox="media/source-control-team-explorer-lrg.png":::</p>1.从“添加到源代码管理”状态栏菜单中选择“Git”。  <br>2.选择“发布”。  | :::image type="content" source="media/source-control-new-git-sml.png" alt-text="Visual Studio 2019 中 Git 选项的屏幕截图拼贴画，其中显示了“添加到源代码管理 - 创建存储库”过程覆盖。" lightbox="media/source-control-new-git-lrg.png":::</p>1.从“添加到源代码管理”状态栏菜单中选择“Git”，或从顶级 Visual Studio 菜单栏中选择“Git”   > “创建 Git 存储库”。 <br>2.选择“创建并推送”。 </p> **注意**：如果要将代码添加到 Azure DevOps，请使用现有的远程选项。 在这种情况下，必须先创建 Azure DevOps 存储库。 |
> [!TIP]
> [新 Git 体验](git-with-visual-studio.md)应根据你打开的存储库或解决方案自动连接到正确的 Azure DevOps 存储库。 但是，如果需要手动连接到存储库，仍可使用团队资源管理器执行此操作。 从 Visual Studio 菜单栏中，选择“查看” > “团队资源管理器” > “管理连接” > “连接”。

## <a name="git-changes"></a>Git 更改

|         |Team Explorer  |新 Git 体验 |
|---------|---------|---------|
|**提交和暂存** | :::image type="content" source="media/commit-stage-team-explorer-sml.png" alt-text="Visual Studio 2019 中团队资源管理器“更改”窗口的屏幕截图，其中包含“提交和暂存”过程覆盖。" lightbox="media/commit-stage-team-explorer-lrg.png":::  </p>1.输入提交消息。 <br>2.选择“全部提交”。 <br>3.若要暂存特定文件，请右键单击该文件，然后选择“暂存”。  | :::image type="content" source="media/commit-stage-new-git-sml.png" alt-text="Visual Studio 2019 中“Git 更改”窗口的屏幕截图，其中包含“提交和暂存”过程覆盖。" lightbox="media/commit-stage-new-git-lrg.png"::: </p>1.输入提交消息。 <br>2.选择“全部提交”。 <br>3.若要暂存特定文件，请将鼠标悬停在其上，然后单击“+”图标。 |
|**修改提交** |  :::image type="content" source="media/amend-commit-team-explorer-sml.png" alt-text="Visual Studio 2019 中团队资源管理器“更改”窗口的屏幕截图，其中包含“修改提交”过程覆盖。" lightbox="media/amend-commit-team-explorer-lrg.png":::</p>1.单击“操作”下拉菜单。 <br>2.选择“修改上一个提交”。 | :::image type="content" source="media/amend-commit-new-git-sml.png" alt-text="Visual Studio 2019 中“Git 更改”窗口的屏幕截图，其中包含“修改提交”过程覆盖。" lightbox="media/amend-commit-new-git-lrg.png"::: </p>1.单击“修改”复选框。 <br>2.单击“全部提交”以提交更新。  |
|**储藏更改** | :::image type="content" source="media/stash-change-team-explorer-sml.png" alt-text="Visual Studio 2019 中团队资源管理器“更改”窗口的屏幕截图，其中包含“储藏更改”过程覆盖。" lightbox="media/stash-change-team-explorer-lrg.png":::</p>1.单击“储藏”下拉菜单。 <br>2.选择相关的“储藏”选项。 | :::image type="content" source="media/stash-change-new-git-sml.png" alt-text="Visual Studio 2019 中“Git 更改”窗口的屏幕截图，其中包含“储藏更改”过程覆盖。" lightbox="media/stash-change-new-git-lrg.png":::</p>1.单击“全部提交”下拉菜单。 <br>2.选择相关的“储藏”选项。 |

## <a name="synchronization"></a>同步

|         |Team Explorer  |新 Git 体验 |
|---------|---------|---------|
|**提取、拉取和推送更改** | :::image type="content" source="media/fetch-pull-push-team-explorer-sml.png" alt-text="Visual Studio 2019 中团队资源管理器“同步”窗口的屏幕截图，其中包含“提取、请求和推送”过程覆盖。" lightbox="media/fetch-pull-push-team-explorer-lrg.png":::</p>1.导航到“同步”页。 <br>2.单击你选择的网络操作。 | :::image type="content" source="media/fetch-pull-push-new-git-sml.png" alt-text="Visual Studio 2019 中“Git 更改”窗口的屏幕截图，其中包含“提取、拉取和推送”过程覆盖。" lightbox="media/fetch-pull-push-team-new-git-lrg.png"::: </p>1.在“Git 更改”窗口中找到“提取”、“拉取”和“推送”按钮。 <br>2.单击你选择的网络操作。|
|**查看传入和传出提交** | :::image type="content" source="media/view-commits-team-explorer-sml.png" alt-text="Visual Studio 2019 中团队资源管理器“同步”窗口的屏幕截图，其中包含“查看传入和传出提交”过程覆盖。" lightbox="media/view-commits-team-explorer-lrg.png"::: </p>1.导航到“同步”页。 <br>2.查看传入和传出列表。 | :::image type="content" source="media/view-commits-new-git-sml.png" alt-text="Visual Studio 2019 中“Git 更改”窗口和“Git 存储库”窗口的屏幕截图，其中包含“查看传入和传出提交”过程覆盖。" lightbox="media/view-commits-new-git-lrg.png":::</p>1.单击“Git 更改”窗口中的“传出/传入”链接。  <br>2.使用“Git 存储库”窗口顶部图表中的图标，查看传入和传出的提交。 |

## <a name="branches"></a>分支

|         |Team Explorer  |新 Git 体验 |
|---------|---------|---------|
|**创建分支** |  :::image type="content" source="media/create-branch-team-explorer-sml.png" alt-text="Visual Studio 2019 中团队资源管理器“分支”窗口的屏幕截图，其中包含“创建新分支”过程覆盖。" lightbox="media/create-branch-team-explorer-lrg.png":::</p>1.导航到“分支”窗口。 <br> 2.单击“新建分支”。 | :::image type="content" source="media/create-branch-new-git-sml.png" alt-text="Visual Studio 2019 中“Git 更改”窗口的屏幕截图，其中包含“创建新分支”过程覆盖。" lightbox="media/create-branch-new-git-lrg.png"::: </p>1.在“Git 更改”窗口中，单击“分支”下拉列表。 <br>2.单击“新建分支”。 |
|**从远程分支获取最新更改** | :::image type="content" source="media/sync-remote-team-explorer-sml.png" alt-text="Visual Studio 2019 中团队资源管理器“分支”窗口的屏幕截图，其中包含“从远程分支获取最新更改”过程覆盖。" lightbox="media/sync-remote-team-explorer-lrg.png"::: </p>1.导航到“分支”页。 <br>2.右键单击远程分支，然后选择“合并自”或“变基到”。   | :::image type="content" source="media/sync-remote-new-git-sml.png" alt-text="Visual Studio 2019 中“Git 更改”窗口的屏幕截图，其中包含“从远程分支获取最新更改”过程覆盖。" lightbox="media/sync-remote-new-git-lrg.png":::</p>1.单击“分支”下拉列表。 <br>2.在“远程”选项卡下，单击远程分支，然后选择“合并到当前分支”或“将当前分支变基到”。    |
|**管理分支** | :::image type="content" source="media/manage-branches-team-explorer-sml.png" alt-text="Visual Studio 2019 中团队资源管理器“分支”窗口的屏幕截图，其中包含“管理分支”过程覆盖。" lightbox="media/manage-branches-team-explorer-lrg.png"::: </p>1.导航到“分支”窗口。 <br>2.右键单击要管理的分支。 <br>3.查看分支的“历史记录”以管理提交。 | :::image type="content" source="media/manage-branches-new-git-sml.png" alt-text="屏幕截图拼贴画显示了如何使用 Visual Studio 2019 中的三个 UI 选项管理分支。" lightbox="media/manage-branches-new-git-lrg.png"::: </p>1.使用以下入口点之一导航到“Git 存储库”窗口： <br><br>a. 从顶级 Visual Studio 菜单中，选择“Git” > “管理分支”。<br> b. 选择“Git 更改” > “传入/传出”。 <br>c. 在右下角的状态栏菜单中，选择“管理分支”。<br> <br> 2.从顶级“Git” > “管理分支”菜单中，执行以下操作之一： <br><br>A. 右键单击分支。<br>B. 选择要管理的提交（多选）。 |

## <a name="conflict-resolution"></a>冲突解决

|         |Team Explorer  |新 Git 体验 |
|---------|---------|---------|
|**访问包含冲突的文件的列表** | :::image type="content" source="media/resolve-conflicts-team-explorer-sml.png" alt-text="Visual Studio 2019 中团队资源管理器“更改”窗口和“解决冲突”窗口的屏幕截图拼贴画，其中包含一个过程覆盖。" lightbox="media/resolve-conflicts-team-explorer-lrg.png":::</p>1.单击“冲突”链接以导航到“解决冲突”窗口。  <br> 2.使用“冲突”列表解决合并冲突。 | :::image type="content" source="media/resolve-conflicts-new-git-sml.png" alt-text="Visual Studio 2019 中“Git 更改”窗口的屏幕截图，其中包含“解决冲突”过程覆盖。" lightbox="media/resolve-conflicts-new-git-lrg.png"::: </p>1.验证是否显示了“合并正在进行中，包含冲突”。 <br>2.“Git 更改”窗口的“未合并的更改”部分将显示具有合并冲突的文件的列表。  <br>解决冲突。 |

## <a name="next-steps"></a>后续步骤

有关新 Git 体验的详细信息，请参阅 YouTube 上的最新视频 [Visual Studio 2019 中的 Git 入门](https://www.youtube.com/watch?v=GCZ9x3yqkyc)。

## <a name="see-also"></a>请参阅

- [Visual Studio 2019 中的 Git 新体验](git-with-visual-studio.md?view=vs-2019&preserve-view=true)
- [Visual Studio 中的 Git 和 GitHub 入门](/learn/modules/visual-studio-github-push/)
- [在 Visual Studio 中使用 GitHub 帐户](../ide/work-with-github-accounts.md)