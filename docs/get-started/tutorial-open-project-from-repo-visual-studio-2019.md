---
title: 教程：在 Visual Studio 2019 中打开存储库中的项目
description: 了解如何使用 Visual Studio 2019 打开 Git 或 Azure DevOps 存储库中的项目。
ms.custom: get-started
ms.date: 02/11/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
author: TerryGLee
ms.author: tglee
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
monikerRange: vs-2019
ms.openlocfilehash: 5a637b2536c05e8f5678989f47dba61cd6ec7381
ms.sourcegitcommit: 15109ead7991f52092502518a6f4d9061cc22cd2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "100335468"
---
# <a name="tutorial-open-a-project-from-a-repo"></a>教程：打开存储库中的项目

在本教程中，你将使用 Visual Studio 首次连接到存储库，然后打开其中的一个项目。

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

## <a name="open-a-project-from-a-github-repo"></a>打开 GitHub 存储库中的项目

使用 Visual Studio 2019 打开 GitHub 存储库中的项目的方式取决于你拥有的版本。 具体来说，如果你已安装 [16.8 版本](/visualstudio/releases/2019/release-notes/)或更高版本，则 Visual Studio 中提供了一个更完全集成的新 [Git 体验](../ide/git-with-visual-studio.md)供你使用。

但无论安装的是哪个版本，你始终可以使用 Visual Studio 打开 GitHub 存储库中的项目。

#### <a name="168-and-later"></a>[16.8 及更高版本](#tab/vs168later)

#### <a name="clone-a-github-repo-and-then-open-a-project"></a>克隆一个 GitHub 存储库，然后打开一个项目

1. 打开 Visual Studio 2019。

1. 在起始窗口中，选择“克隆存储库”。

   ![Visual Studio 2019 版本 16.8 及更高版本中“克隆存储库”对话框的屏幕截图](../ide/media/vs-2019/clone-repository.png)

1. 输入或键入存储库位置，然后选择“克隆”。

   ![Visual Studio 2019 版本 16.8 及更高版本中，在其中输入 Git 存储库 URL 的“克隆存储库”对话框的屏幕截图](../ide/media/vs-2019/clone-repository-enter-location.png)

1. 系统可能会要求你在“Git 用户信息”对话框中提供用户登录信息。 可添加你的信息或编辑所提供的默认信息。

   ![Visual Studio 2019 版本 16.8 及更高版本中，在其中输入或编辑帐户信息的“Git 用户信息”对话框的屏幕截图](../ide/media/vs-2019/git-user-information-dialog.png)

    选择“保存”，将信息添加到全局 .gitconfig 文件。 （或可以选择“取消”，之后再执行此操作。）

    接下来，Visual Studio 自动从存储库中加载并打开解决方案。

   ![Visual Studio 2019 版本 16.8 及更高版本中，已在解决方案资源管理器中打开的 Git 中一个项目的屏幕截图](../ide/media/vs-2019/git-solution-explorer.png )

1. 如果存储库包含多个解决方案，你将在解决方案资源管理器中看到它们。 选择解决方案资源管理器中的“切换视图”按钮，可查看解决方案列表。

   ![Visual Studio 2019 版本 16.8 及更高版本中，已在解决方案资源管理器中打开的 Git 中一个项目的屏幕截图，其中突出显示了“切换视图”按钮](../ide/media/vs-2019/git-solution-explorer-switch-views.png)

   然后，解决方案资源管理器为你提供了选择 - 在“文件夹视图”中打开根文件夹，还是选择一个要打开的解决方案文件。

   ![Visual Studio 2019 版本 16.8 及更高版本中，选择“切换视图”按钮后，已在解决方案资源管理器中打开的 Git 中的 .sln 文件屏幕截图](../ide/media/vs-2019/git-solution-explorer-view-solution.png)

    若要切换视图，请再次选择“切换视图”按钮。

    > [!TIP]
    > 你还可以使用 Visual Studio IDE 中的“Git”菜单来克隆存储库并打开项目。
    >
    > ![Visual Studio 2019 版本 16.8 及更高版本中“Git”菜单的屏幕截图](../ide/media/vs-2019/git-menu-clone-create-git-repository.png)

#### <a name="open-a-project-locally-from-a-previously-cloned-github-repo"></a>在本地打开之前克隆的 GitHub 存储库中的项目

1. 打开 Visual Studio 2019。

1. 在起始窗口中，选择“打开项目或解决方案”。

    Visual Studio 将打开文件资源管理器的一个实例，你可以在其中浏览到你的解决方案或项目，然后选择它以将其打开。

   ![Visual Studio 2019 版本 16.8 及更高版本中“打开项目或解决方案”窗口的屏幕截图](../ide/media/vs-2019/open-local-project-from-cloned-repo.png)

    如果最近打开过该项目或解决方案，可从“打开最近使用的文件”部分中将其选中，快速地再次将其打开。

    > [!TIP]
    > 你还可以使用 Visual Studio IDE 中的“Git”菜单，打开之前已克隆的存储库中的本地文件夹和文件。
    >
    > ![Visual Studio 2019 版本 16.8 及更高版本中“Git”菜单的屏幕截图，其中“本地存储库”选项已展开](../ide/media/vs-2019/git-menu-local-repositories.png)

    开始编码！

#### <a name="167-and-earlier"></a>[16.7 及更低版本](#tab/vs167earlier)

#### <a name="clone-a-github-repo-and-then-open-a-project"></a>克隆一个 GitHub 存储库，然后打开一个项目

1. 打开 Visual Studio 2019。

1. 在起始窗口上，选择“克隆或签出代码”。

   ![Visual Studio 2019 版本 16.7 及更低版本中“新建项目”窗口的屏幕截图](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. 输入或键入存储库位置，然后选择“克隆”。

   ![Visual Studio 2019 版本 16.7 及更低版本中“克隆或签出代码”窗口的屏幕截图](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   Visual Studio 从存储库打开项目。

1. 如果有可用的解决方案文件，它会显示在“解决方案和文件夹”弹出菜单中。 选择它后，Visual Studio 将打开你的解决方案。

   ![Visual Studio 2019 版本 16.7 及更低版本中，解决方案资源管理器下拉列表的屏幕截图](./media/open-proj-repo-github-solutions-folders-picker.png)

   如果存储库中没有解决方案文件（具体是 .sln 文件），弹出菜单显示“未找到解决方案”。 但是，可以双击文件夹菜单中的任意文件，以便在 Visual Studio 代码编辑器中将其打开。

    开始编码！

---

> [!NOTE]
> 有关特定于 Visual Studio 2017 的信息，请参阅[在 Visual Studio 2017 中打开存储库中的项目](tutorial-open-project-from-repo-visual-studio-2017.md)页面。

## <a name="connect-to-an-azure-devops-server"></a>连接到 Azure DevOps Server

使用 Visual Studio 2019 连接到 Azure DevOps Server 时看到的内容取决于你拥有的版本。 具体来说，如果你已安装 [16.8 版本](/visualstudio/releases/2019/release-notes/)或更高版本，我们已更改了 UI，以适应 Visual Studio 中更全面集成的全新 [Git 体验](../ide/git-with-visual-studio.md)。

但无论安装的是哪个版本，你始终可以使用 Visual Studio 连接到 Azure DevOps Server。

#### <a name="168-and-later"></a>[16.8 及更高版本](#tab/vs168later)

1. 打开 Visual Studio 2019。

1. 在起始窗口中，选择“克隆存储库”。

   ![Visual Studio 2019 版本 16.8 及更高版本中，针对 Azure DevOps 的“克隆存储库”对话框的屏幕截图](../ide/media/vs-2019/clone-repository.png)

1. 在“浏览存储库”部分中，选择“Azure DevOps” 。

    ![Visual Studio 2019 版本 16.8 及更高版本中，“连接到项目”对话框的“浏览存储库”部分的屏幕截图](../ide/media/vs-2019/browse-repository-azure-devops.png)

1. 如果看到登录窗口，请登录帐户。

1. 在“连接到项目”对话框中，选择要连接的存储库，然后选择“克隆” 。

      ![从 Visual Studio 2019 版本 16.8 及更高版本生成的“连接到项目”对话框的屏幕截图](../ide/media/vs-2019/connect-project-azure-devops.png)

      > [!TIP]
      > 如果未看到要连接的存储库的预填充列表，选择“添加 Azure DevOps Server”，输入一个服务器 URL。 （或者，你可能会看到“找不到任何服务器”提示，其中包含用于添加现有 Azure DevOps Server 或创建 Azure DevOps 帐户的链接。）

   接下来，Visual Studio 将打开解决方案资源管理器，其中显示了这些文件夹和文件。

1. 选择“团队资源管理器”选项卡以查看 Azure DevOps 操作。

      ![从 Visual Studio 2019 版本 16.8 及更高版本生成的“团队资源管理器”对话框的屏幕截图](../ide/media/vs-2019/team-explorer-azure-devops.png)

#### <a name="167-and-earlier"></a>[16.7 及更低版本](#tab/vs167earlier)

1. 打开 Visual Studio 2019。

1. 在起始窗口上，选择“克隆或签出代码”。

   ![Visual Studio 2019 版本 16.7 及更低版本中“新建项目”窗口的屏幕截图](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. 在“浏览存储库”部分中，选择“Azure DevOps” 。

   ![Visual Studio 2019 版本 16.7 及更低版本中“克隆或签出代码”窗口的屏幕截图，其中“浏览存储库”部分列出了 Azure DevOps](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   如果看到登录窗口，请登录帐户。

1. 在“连接到项目”对话框中，选择要连接的存储库，然后选择“克隆” 。

      ![从 Visual Studio 2019 版本 16.7 及更低版本生成的“连接到项目”对话框的屏幕截图](./media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > 列表框中显示的内容取决于你有权访问的 Azure DevOps 存储库。

   克隆完成后，Visual Studio 会打开“团队资源管理器”并显示通知。

     ![Visual Studio 2019 版本 16.7 及更低版本中，克隆完成后“团队资源管理器”窗口的屏幕截图](./media/vs-2019/clone-complete-azure-devops.png)

1. 若要查看文件夹和文件，请选择“显示文件夹视图”链接。

     ![Visual Studio 2019 版本 16.7 及更低版本中，克隆完成后“团队资源管理器”窗口“解决方案”部分的屏幕截图](./media/vs-2019/show-folder-view-azure-devops.png)

     Visual Studio 随即打开“解决方案资源管理器”。

1. 选择“解决方案和文件夹”链接，搜索要打开的解决方案文件（具体是 .sln 文件）。

      ![Visual Studio 2019 版本 16.7 及更低版本中，团队资源管理器中“解决方案和文件夹”通知的屏幕截图](./media/open-proj-repo-solutions-folders.png)

   如果存储库中没有解决方案文件，则会显示消息“找不到解决方案”。 但是，可以双击文件夹菜单中的任意文件，以便在 Visual Studio 代码编辑器中将其打开。

---

## <a name="next-steps"></a>后续步骤

如果你已准备好使用 Visual Studio 进行编码，请深入了解以下特定于语言的任何教程：

- [Visual Studio 教程 | C#](./csharp/index.yml)
- [Visual Studio 教程 | Visual Basic](./visual-basic/index.yml)
- [Visual Studio 教程 | C++](/cpp/get-started/tutorial-console-cpp)
- [Visual Studio 教程 | Python](../python/index.yml)
- [Visual Studio 教程 | JavaScript、TypeScript 和 Node.js](../javascript/index.yml)

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 2017 中打开存储库中的项目](tutorial-open-project-from-repo-visual-studio-2017.md)
- [Visual Studio 2019 中的 Git 新体验](../ide/git-with-visual-studio.md)
- [Azure DevOps Services：Azure Repos 和 Visual Studio 入门](/azure/devops/repos/git/gitquickstart/)
- [Microsoft Learn：Azure DevOps 入门](/learn/modules/get-started-with-devops/)