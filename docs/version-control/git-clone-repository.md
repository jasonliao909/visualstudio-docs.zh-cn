---
title: 在 Visual Studio 中克隆存储库
titleSuffix: ''
description: 使用 Git 或 Azure DevOps 在 Visual Studio 中克隆存储库。
ms.date: 11/08/2021
ms.topic: how-to
author: TerryGLee
ms.author: tglee
ms.manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: 5fc34f78236b3f79f44e80a8be8faef66e235a58
ms.sourcegitcommit: 67dc39e93c86ba50eb5ca877b0471fb8ab8475ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2021
ms.locfileid: "132001747"
---
# <a name="clone-a-repo-in-visual-studio"></a>在 Visual Studio 中克隆存储库

通过 Visual Studio 可以轻松从 IDE 中克隆 GitHub 存储库或 Azure DevOps 存储库。 你还可以在执行此操作时登录到 GitHub 或 Azure DevOps。 操作方法如下。

## <a name="clone-a-github-repo-and-sign-in"></a>克隆 GitHub 存储库并登录

1. 打开 Visual Studio。

1. 从“Git”菜单中，选择“克隆存储库” 。

    :::image type="content" source="../ide/media/vs-2022/git-menu-clone-repository.png" alt-text="Visual Studio 中 Git 菜单上的“克隆存储库”选项的屏幕截图。":::

    > [!NOTE]
    > 如果之前尚未与 Git 菜单交互，你可能会看到“克隆”，而不是“克隆存储库”  。 如果出现这种情况，请选择“克隆”。

1. 在“克隆存储库”窗口中的“输入 Git 存储库 URL”部分下，将存储库信息添加到“存储库位置”框中  。

    接下来，在“路径”部分中，可以选择接受本地源文件的默认路径，也可以选择浏览到其他位置。

    然后，在“浏览存储库”部分中，选择 GitHub 。

    :::image type="content" source="media/vs-2022/git-menu-clone-repo-dialog.png" alt-text="“克隆存储库”对话框的屏幕截图，其中突出显示了 GitHub。":::

1. 在“从 GitHub 打开”窗口中，可以验证 GitHub 帐户信息，也可以添加信息。 为此，请从下拉菜单中选择“登录”。

    :::image type="content" source="media/vs-2022/git-menu-clone-repo-dialog-github-account.png" alt-text="“从 GitHub 打开”窗口中“登录”下拉部分的屏幕截图。":::

    如果你是首次从 Visual Studio 登录到 GitHub，则会出现“授权 Visual Studio”通知。 选择所需的选项，然后选择“授权 GitHub”。

    :::image type="content" source="media/vs-2022/git-menu-github-authorize-visual-studio-sml.png" alt-text="授权对话框的屏幕截图。" lightbox="media/vs-2022/git-menu-github-authorize-visual-studio-lrg.png":::

    接下来，你将看到一个授权确认窗口。 输入密码，然后选择“确认密码”。

    :::image type="content" source="media/vs-2022/git-menu-github-authorize-confirm-access-sml.png" alt-text="确认访问对话框的屏幕截图。" lightbox="media/vs-2022/git-menu-github-authorize-confirm-access-lrg.png":::

    将 GitHub 帐户与 Visual Studio 链接后，将显示成功通知。

    :::image type="content" source="../ide/media/github-success-signin.png" alt-text="将 GitHub 帐户与 Visual Studio 链接后收到的成功通知的屏幕截图。":::

1. 登录后，Visual Studio 返回到“克隆存储库”对话框，在该对话框中，“从 GitHub 打开”窗口将列出你有权访问的所有存储库 。 选择所需的项，然后选择“克隆”。

    如果未显示存储库列表，请输入存储库的位置，然后选择“克隆”。

    :::image type="content" source="media/vs-2022/git-menu-clone-repo-dialog-open-from-github-location-sml.png" alt-text="“从 GitHub 打开”窗口的屏幕截图，可在其中选择存储库或添加存储库。" lightbox="media/vs-2022/git-menu-clone-repo-dialog-open-from-github-location-lrg.png":::

1. 接下来，Visual Studio 会显示存储库中的解决方案列表。 选择要加载的解决方案，或在[解决方案资源管理器](../ide/use-solution-explorer.md?view=vs-2022&preserve-view=true)中打开“文件夹视图” 。

    :::image type="content" source="../ide/media/vs-2022/git-solution-explorer-folder-view.png" alt-text="屏幕截图，显示 Visual Studio 2022 的解决方案资源管理器中的“文件夹视图”。":::

    > [!TIP]
    > 可以通过 Git 菜单将默认“文件夹视图”更改为“解决方案视图”。 选择“设置” > “源代码管理” > “Git 全局设置” > “打开 Git 存储库时自动加载解决方案”，以执行该操作。

### <a name="open-an-existing-local-repository"></a>打开现有的本地存储库

克隆存储库或[创建存储库](git-create-repository.md)之后，Visual Studio 将检测该 Git 存储库，并将其添加到 Git 菜单中的“本地存储库”列表。 在这里，你可以快速访问 Git 存储库并在其之间快速切换。

## <a name="browse-to-and-then-clone-an-azure-devops-repo"></a>浏览到 Azure DevOps 存储库并进行克隆

1. 打开 Visual Studio。

1. 从 Git 菜单中，选择“克隆存储库” 。

    :::image type="content" source="media/vs-2022/git-menu-clone-repository.png" alt-text="Visual Studio 中 Git 菜单上的完整“克隆存储库”选项的屏幕截图。":::

1. 在“克隆存储库”对话框的“浏览存储库”部分，选择 Azure DevOps  。

    :::image type="content" source="../ide/media/vs-2022/browse-repository-azure-devops.png" alt-text="Visual Studio 中“克隆存储库”对话框的“浏览存储库”部分的屏幕截图，突出显示了 Azure DevOps。":::

1. 此时将出现“连接到项目”对话框。 按照提示登录到你的 Azure 帐户，然后浏览到要查找的文件所在的 Azure DevOps Server。

## <a name="next-steps"></a>后续步骤

若要继续学习，请访问[创建存储库](git-create-repository.md)页面。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 Git 体验](../ide/git-with-visual-studio.md)
- [教程：打开存储库中的项目](../get-started/tutorial-open-project-from-repo.md)
- [在 Visual Studio 中使用 GitHub 帐户](../ide/work-with-github-accounts.md)
- [使用多个用户帐户](../ide/work-with-multiple-user-accounts.md)
- [登录 Visual Studio](../ide/signing-in-to-visual-studio.md)