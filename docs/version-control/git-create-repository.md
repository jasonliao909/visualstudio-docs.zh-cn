---
title: 在 Visual Studio 中创建存储库
titleSuffix: ''
description: 使用 Git 在 Visual Studio 中创建存储库，或浏览到 Azure DevOps 存储库。
ms.date: 11/10/2021
ms.topic: how-to
author: TerryGLee
ms.author: tglee
ms.manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: 3ef08c327e7fb0945338477f2a971a0decb364eb
ms.sourcegitcommit: dc12d3d0ca2ec3601cb9de7c22e61ecf22c7c514
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2021
ms.locfileid: "132264156"
---
# <a name="create-a-repo-in-visual-studio"></a>在 Visual Studio 中创建存储库

使用 Visual Studio 可以轻松从 IDE 克隆存储库。 操作方法如下。

## <a name="create-a-github-repo"></a>创建 GitHub 存储库

1. 打开 Visual Studio，然后选择“创建新项目”。

    > [!TIP]
    > 如果 Visual Studio 中尚未拥有添加到存储库的项目，可以快速[创建新的 C# 控制台应用](../get-started/csharp/tutorial-console.md#create-a-project)，并将其命名为 MyNewApp。 Visual Studio 使用默认的“Hello, World!”代码填充 新应用。

1. 从 Git 菜单中，选择“创建存储库” 。

    :::image type="content" source="media/vs-2022/git-menu-create-git-repository.png" alt-text="Visual Studio 中 Git 菜单上的“创建存储库”选项的屏幕截图。":::

1. 在“创建 Git 存储库”对话框中的“推送到新的远程存储库”部分下，选择 GitHub  。

    :::image type="content" source="media/vs-2022/git-menu-create-github-repo-dialog.png" alt-text="Visual Studio 中 Git 菜单的“创建 Git 存储库”选项的屏幕截图，其中突出显示了 GitHub 选项。":::

1. 在“创建 Git 存储库”对话框的“创建新的 GitHub 存储库”部分中，输入要创建的存储库的名称 。

    > [!TIP]
    > 如果尚未登录到 GitHub 帐户，也可以在此屏幕中登录。

1. 登录并输入存储库信息后，选择“创建并推送”按钮以创建存储库并添加应用。

    :::image type="content" source="media/vs-2022/git-menu-create-git-repo-push-code.png" alt-text="使用“创建 Git 存储库”窗口输入的用户的 GitHub 信息的屏幕截图。":::

### <a name="open-an-existing-local-repository"></a>打开现有的本地存储库

创建存储库或[克隆存储库](git-clone-repository.md)之后，Visual Studio 将检测该 Git 存储库，并将其添加到 Git 菜单中的“本地存储库”列表。 在这里，你可以快速访问 Git 存储库并在其之间快速切换。

## <a name="create-an-azure-devops-repo"></a>创建 Azure DevOps 存储库

1. 打开 Visual Studio，然后选择“创建新项目”。

    > [!TIP]
    > 如果 Visual Studio 中尚未拥有添加到存储库的项目，可以快速[创建新的 C# 控制台应用](../get-started/csharp/tutorial-console.md#create-a-project)，并将其命名为 MyNewApp。 Visual Studio 使用默认的“Hello, World!”代码填充 新应用。

1. 从 Git 菜单中，选择“创建存储库” 。

1. 在“创建 Git 存储库”对话框中的“推送到新的远程存储库”部分下，选择 Azure DevOps  。

1. 在“创建新的 Azure DevOps 存储库”部分中，登录到 Azure 帐户，然后从“项目”下拉列表中选择一个项目 。

1. 选择“创建并推送”按钮以创建存储库并添加应用。

    :::image type="content" source="media/vs-2022/git-menu-publish-azure-devops.png" alt-text="“创建 Git 存储库”对话框的“创建和推送”功能的屏幕截图，可用于通过单个操作发布代码。":::

## <a name="next-steps"></a>后续步骤

若要继续学习，请访问[创建分支](git-create-branch.md)页面。

## <a name="see-also"></a>请参阅

- [教程：打开存储库中的项目](../get-started/tutorial-open-project-from-repo.md)
- [在 Visual Studio 中使用 GitHub 帐户](../ide/work-with-github-accounts.md)
- [使用多个用户帐户](../ide/work-with-multiple-user-accounts.md)
- [登录 Visual Studio](../ide/signing-in-to-visual-studio.md)
- [Visual Studio 和 GitHub：更好地协同工作](https://visualstudio.microsoft.com/vs/github/)