---
title: 教程：在 Visual Studio 中打开存储库中的项目
description: 了解如何使用 Visual Studio 打开 Git 或 Azure DevOps 存储库中的项目。
ms.custom: vs-acquisition, get-started
ms.date: 11/11/2021
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
ms.openlocfilehash: 619a9cacfdf272bb6b76e0115b90edddf2c73180
ms.sourcegitcommit: d38d1b083322019663fec7d1d85a4cda456aadca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2021
ms.locfileid: "135534159"
---
# <a name="tutorial-open-a-project-from-a-repo"></a>教程：打开存储库中的项目

在本教程中，你将使用 Visual Studio 首次连接到存储库，然后打开其中的一个项目。

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker range="vs-2022"

## <a name="open-a-project-from-a-github-repo"></a>打开 GitHub 存储库中的项目

可以使用 Visual Studio 轻松打开存储库中的项目。 可以在启动 Visual Studio 时执行此操作，也可以直接从 [Visual Studio IDE](visual-studio-ide.md?view=vs-2022&preserve-view=true) 中执行此操作。

操作方法如下。

### <a name="use-the-start-window"></a>使用“开始”窗口

1. 打开 Visual Studio。

1. 在起始窗口中，选择“克隆存储库”。

    :::image type="content" source="../ide/media/vs-2022/clone-repository.png" alt-text="Visual Studio 中“克隆存储库”对话框的屏幕截图。":::

1. 输入或键入存储库位置，然后选择“克隆”按钮。

    :::image type="content" source="../ide/media/vs-2022/clone-repository-enter-location.png" alt-text="&quot;克隆存储库&quot; 对话框的屏幕截图，可在其中输入 Git 存储库 URL Visual Studio。":::

1. 系统可能会要求你在“Git 用户信息”对话框中提供用户登录信息。 可添加你的信息或编辑所提供的默认信息。

    :::image type="content" source="../ide/media/vs-2022/git-user-information-dialog.png" alt-text="Visual Studio 2022 中的“Git 用户信息”对话框（在其中输入或编辑帐户信息）的屏幕截图。":::

    选择“保存”，将信息添加到全局 .gitconfig 文件。 （或可以选择“取消”，之后再执行此操作。）

    > [!TIP]
    > 有关登录 Visual Studio 的详细信息，请参阅[登录 Visual Studio](../ide/signing-in-to-visual-studio.md?view=vs-2022&preserve-view=true) 页。 有关如何使用 GitHub 帐户进行登录的具体信息，请参阅[在 Visual Studio 中使用 GitHub 帐户](../ide/work-with-github-accounts.md?view=vs-2022&preserve-view=true)页。 如果你收到信任通知，想要了解有关它的详细信息，请参阅[配置文件和文件夹的信任设置](../ide/reference/trust-settings.md?view=vs-2022&preserve-view=true)页。

### <a name="view-files-in-solution-explorer"></a>解决方案资源管理器中的的视图文件

1. 接下来，Visual Studio 会通过使用[解决方案资源管理器](../ide/use-solution-explorer.md?view=vs-2022&preserve-view=true)中的“文件夹视图”，从存储库加载解决方案。 

    :::image type="content" source="../ide/media/vs-2022/git-solution-explorer-folder-view.png" alt-text="屏幕截图，显示 Visual Studio 2022 的解决方案资源管理器中的“文件夹视图”。":::

    可以在“解决方案视图”中查看某个解决方案，方法是双击其 .sln 文件。

    也可以选择“切换视图”按钮，然后选择“Program.cs”来查看解决方案的代码。 

    :::image type="content" source="../ide/media/vs-2022/git-solution-explorer-switch-views.png" alt-text="Git 中某个项目的屏幕截图，该项目在 Visual Studio 2022 的解决方案资源管理器中打开，其中突出显示了“切换视图”按钮。":::

> [!TIP]
> 默认视图设置为“文件夹视图”。 可以通过“Git”菜单将其更改为“解决方案视图”。 选择“设置” > “源代码管理” > “Git 全局设置” > “打开 Git 存储库时自动加载解决方案”，以执行该操作。

#### <a name="open-a-project-locally-from-a-previously-cloned-github-repo"></a>在本地打开之前克隆的 GitHub 存储库中的项目

1. 打开 Visual Studio。

1. 在起始窗口中，选择“打开项目或解决方案”。

    Visual Studio 将打开文件资源管理器的一个实例，你可以在其中浏览到你的解决方案或项目，然后选择它以将其打开。

    :::image type="content" source="../ide/media/vs-2022/open-local-project-from-cloned-repo.png" alt-text="Visual Studio 2022 中“打开项目或解决方案”窗口的屏幕截图。":::

    > [!TIP]
    > 如果最近打开过该项目或解决方案，可从“打开最近使用的文件”部分中将其选中，快速地再次将其打开。

    开始编码！

### <a name="use-the-ide"></a>使用 IDE

还可以在 Visual Studio IDE 中使用“Git”菜单或“选择存储库”控件，与存储库的文件夹和文件进行交互。

操作方法如下。

#### <a name="to-clone-a-repo-and-open-a-project"></a>克隆存储库并打开项目

1. 在 Visual Studio IDE 中选择“Git”菜单，然后选择“克隆存储库”。

    :::image type="content" source="../ide/media/vs-2022/git-menu-clone-repository.png" alt-text="Visual Studio 2022 中的“Git”菜单的屏幕截图，其中已选中“克隆存储库”。":::

1. 按照提示连接到包含要查找的文件的 Git 存储库。

#### <a name="to-open-local-folders-and-files"></a>打开本地文件夹和文件

1. 在 Visual Studio IDE 中依次选择“Git”菜单、“本地存储库”、“打开本地存储库”  。

    :::image type="content" source="../ide/media/vs-2022/git-menu-local-repositories.png" alt-text="Visual Studio 2022 中的“Git”菜单的屏幕截图，其中显示了“本地存储库”和“打开本地存储库”。":::

    也可从“解决方案资源管理器”执行同一任务。 为此，请依次选择“选择存储库”控件、“筛选存储库”框旁边的省略号图标、“打开本地存储库”。   

    :::image type="content" source="../ide/media/vs-2022/select-repository-filter-ellipsis.png" alt-text="“选择存储库”控件的屏幕截图，其中选中了省略号图标并显示了“打开本地存储库”选项。":::

1. 按照提示连接到包含要查找的文件的 Git 存储库。

## <a name="browse-to-an-azure-devops-repo"></a>浏览到 Azure DevOps 存储库

下面介绍如何使用 Visual Studio 浏览到并克隆 Azure DevOps 存储库。

1. 打开 Visual Studio。

1. 在起始窗口中，选择“克隆存储库”。

    :::image type="content" source="../ide/media/vs-2022/clone-repository.png" alt-text="Visual Studio 中用于 Azure DevOps 的“克隆存储库”对话框的屏幕截图。":::

1. 在“浏览存储库”部分中，选择“Azure DevOps” 。

    :::image type="content" source="../ide/media/vs-2022/browse-repository-azure-devops.png" alt-text="Visual Studio 中“克隆存储库”对话框的“浏览存储库”部分的屏幕截图，突出显示了 Azure DevOps。":::

1. 按照提示克隆要查找的文件所在的 Azure DevOps 存储库，然后打开你的项目。

::: moniker-end

::: moniker range="vs-2019"

## <a name="open-a-project-from-a-github-repo-with-visual-studio-2019"></a>使用 Visual Studio 2019 打开 GitHub 存储库中的项目

使用 Visual Studio 打开 GitHub 存储库中的项目的方式取决于你的版本。 具体来说，如果你已安装 Visual Studio 2019 [版本 16.8](/visualstudio/releases/2019/release-notes-history) 或更高版本，则可使用 Visual Studio 中提供的一个更全面集成的全新 [Git 体验](../version-control/git-with-visual-studio.md)。

但无论安装的是哪个版本，你始终可以使用 Visual Studio 打开 GitHub 存储库中的项目。

### <a name="visual-studio-2019-version-168-and-later"></a>Visual Studio 2019 版本 16.8 及更高版本

下面介绍了如何使用 Visual Studio 2019 [版本 16.8](/visualstudio/releases/2019/release-notes-history) 或更高版本中的 Git。

#### <a name="clone-a-github-repo-and-then-open-a-project"></a>克隆一个 GitHub 存储库，然后打开一个项目

1. 打开 Visual Studio 2019。

1. 在起始窗口中，选择“克隆存储库”。

   ![Visual Studio 2019 版本 16.8 及更高版本中“克隆存储库”对话框的屏幕截图](../ide/media/vs-2019/clone-repository.png)

1. 输入或键入存储库位置，然后选择“克隆”。

   ![Visual Studio 2019 版本 16.8 及更高版本中“克隆存储库”对话框（你在其中输入 Git 存储库 URL）的屏幕截图。](../ide/media/vs-2019/clone-repository-enter-location.png)

1. 系统可能会要求你在“Git 用户信息”对话框中提供用户登录信息。 可添加你的信息或编辑所提供的默认信息。

   ![Visual Studio 2019 版本 16.8 及更高版本中“Git 用户信息”对话框（你在其中输入或编辑帐户信息）的屏幕截图。](../ide/media/vs-2019/git-user-information-dialog.png)

    选择“保存”，将信息添加到全局 .gitconfig 文件。 （或可以选择“取消”，之后再执行此操作。）

    > [!TIP]
    > 有关登录 Visual Studio 的详细信息，请参阅[登录 Visual Studio](../ide/signing-in-to-visual-studio.md?view=vs-2019&preserve-view=true) 页面。 有关如何使用 GitHub 帐户登录的特定信息，请参阅[在 Visual Studio 中使用 GitHub 帐户](../ide/work-with-github-accounts.md?view=vs-2019&preserve-view=true)页面。

    接下来，Visual Studio 自动从存储库中加载并打开解决方案。

   ![已在 Visual Studio 2019 版本 16.8 及更高版本中的解决方案资源管理器内打开的 Git 中的一个项目的屏幕截图。](../ide/media/vs-2019/git-solution-explorer.png )

1. 如果存储库包含多个解决方案，你将在解决方案资源管理器中看到它们。 选择解决方案资源管理器中的“切换视图”按钮，可查看解决方案列表。

   ![已在 Visual Studio 2019 版本 16.8 及更高版本中的解决方案资源管理器内打开的 Git 中的一个项目的屏幕截图，其中突出显示了“切换视图”按钮。](../ide/media/vs-2019/git-solution-explorer-switch-views.png)

   然后，解决方案资源管理器为你提供了选择 - 在“文件夹视图”中打开根文件夹，还是选择一个要打开的解决方案文件。

   ![Visual Studio 2019 版本 16.8 及更高版本中，选择“切换视图”按钮后，Git 中的 .sln 文件（已在解决方案资源管理器中打开）的屏幕截图。](../ide/media/vs-2019/git-solution-explorer-view-solution.png)

    若要切换视图，请再次选择“切换视图”按钮。

    > [!TIP]
    > 你还可以使用 Visual Studio IDE 中的“Git”菜单来克隆存储库并打开项目。
    >
    > ![Visual Studio 2019 版本 16.8 及更高版本中“Git”菜单的屏幕截图。](../ide/media/vs-2019/git-menu-clone-create-git-repository.png)

#### <a name="open-a-project-locally-from-a-previously-cloned-github-repo"></a>在本地打开之前克隆的 GitHub 存储库中的项目

1. 打开 Visual Studio 2019 版本 16.8 或更高版本。

1. 在起始窗口中，选择“打开项目或解决方案”。

    Visual Studio 将打开文件资源管理器的一个实例，你可以在其中浏览到你的解决方案或项目，然后选择它以将其打开。

   ![Visual Studio 2019 版本 16.8 及更高版本中“打开项目或解决方案”窗口的屏幕截图。](../ide/media/vs-2019/open-local-project-from-cloned-repo.png)

    如果最近打开过该项目或解决方案，可从“打开最近使用的文件”部分中将其选中，快速地再次将其打开。

    > [!TIP]
    > 你还可以使用 Visual Studio IDE 中的“Git”菜单，打开之前已克隆的存储库中的本地文件夹和文件。
    >
    > ![Visual Studio 2019 版本 16.8 及更高版本中“Git”菜单的屏幕截图，其中的“本地存储库”选项已展开。](../ide/media/vs-2019/git-menu-local-repositories.png)

    开始编码！

### <a name="visual-studio-2019-version-167-and-earlier"></a>Visual Studio 2019 版本 16.7 及更早版本

下面介绍如何使用 Visual Studio 2019 [版本 16.7](/visualstudio/releases/2019/release-notes-history) 或更低版本中的 Git。

#### <a name="clone-a-github-repo-and-then-open-a-project"></a>克隆一个 GitHub 存储库，然后打开一个项目

1. 打开 Visual Studio 2019 版本 16.7 或更低版本。

1. 在起始窗口上，选择“克隆或签出代码”。

   ![Visual Studio 2019 版本 16.7 及更低版本中“新建项目”窗口的屏幕截图。](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. 输入或键入存储库位置，然后选择“克隆”。

   ![Visual Studio 2019 版本 16.7 及更低版本中“克隆或签出代码”窗口的屏幕截图。](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   Visual Studio 从存储库打开项目。

1. 如果有可用的解决方案文件，它会显示在“解决方案和文件夹”弹出菜单中。 选择它后，Visual Studio 将打开你的解决方案。

   ![Visual Studio 2019 版本 16.7 及更低版本中“解决方案资源管理器”下拉列表的屏幕截图。](./media/open-proj-repo-github-solutions-folders-picker.png)

   如果存储库中没有解决方案文件（具体是 .sln 文件），弹出菜单显示“未找到解决方案”。 但是，可以双击文件夹菜单中的任意文件，以便在 Visual Studio 代码编辑器中将其打开。

    开始编码！

## <a name="browse-to-an-azure-devops-repo-with-visual-studio-2019"></a>使用 Visual Studio 2019 浏览到 Azure DevOps 存储库

使用 Visual Studio 2019 浏览到并克隆 Azure DevOps 存储库时看到的内容取决于你的版本。 具体来说，如果你已安装 [16.8 版本](/visualstudio/releases/2019/release-notes-history)或更高版本，我们已更改了 UI，以适应 Visual Studio 中更全面集成的全新 [Git 体验](../version-control/git-with-visual-studio.md)。

但无论安装的是哪个版本，你始终可以使用 Visual Studio 浏览到并克隆 Azure DevOps 存储库。

### <a name="visual-studio-2019-version-168-and-later"></a>Visual Studio 2019 版本 16.8 及更高版本

1. 打开 Visual Studio 2019 [版本 16.8](/visualstudio/releases/2019/release-notes-history) 或更高版本。

1. 在起始窗口中，选择“克隆存储库”。

   ![Visual Studio 2019 版本 16.8 及更高版本中用于 Azure DevOps 的“克隆存储库”对话框的屏幕截图。](../ide/media/vs-2019/clone-repository.png)

1. 在“浏览存储库”部分中，选择“Azure DevOps” 。

    ![Visual Studio 2019 版本 16.8 及更高版本中“连接到项目”对话框的“浏览存储库”部分的屏幕截图。](../ide/media/vs-2019/browse-repository-azure-devops.png)

1. 如果看到登录窗口，请登录帐户。

1. 在“连接到项目”对话框中，选择要连接的存储库，然后选择“克隆” 。

      ![从 Visual Studio 2019 版本 16.8 及更高版本生成的“连接到项目”对话框的屏幕截图。](../ide/media/vs-2019/connect-project-azure-devops.png)

      > [!TIP]
      > 如果未看到要连接的存储库的预填充列表，选择“添加 Azure DevOps Server”，输入一个服务器 URL。 （或者，你可能会看到“找不到任何服务器”提示，其中包含用于添加现有 Azure DevOps Server 或创建 Azure DevOps 帐户的链接。）

   接下来，Visual Studio 将打开解决方案资源管理器，其中显示了这些文件夹和文件。

1. 选择“团队资源管理器”选项卡以查看 Azure DevOps 操作。

      ![从 Visual Studio 2019 版本 16.8 及更高版本生成的“团队资源管理器”对话框的屏幕截图。](../ide/media/vs-2019/team-explorer-azure-devops.png)

#### <a name="visual-studio-2019-version-167-and-earlier"></a>Visual Studio 2019 版本 16.7 及更早版本

1. 打开 Visual Studio 2019 [版本 16.7](/visualstudio/releases/2019/release-notes-history) 或更低版本。

1. 在起始窗口上，选择“克隆或签出代码”。

   ![Visual Studio 2019 版本 16.7 及更低版本中“新建项目”窗口的屏幕截图。](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. 在“浏览存储库”部分中，选择“Azure DevOps” 。

   ![Visual Studio 2019 版本 16.7 及更低版本中“克隆或签出代码”窗口的屏幕截图，其中的“浏览存储库”部分列出了 Azure DevOps。](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   如果看到登录窗口，请登录帐户。

1. 在“连接到项目”对话框中，选择要连接的存储库，然后选择“克隆” 。

      ![从 Visual Studio 2019 版本 16.7 及更低版本生成的“连接到项目”对话框的屏幕截图。](./media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > 列表框中显示的内容取决于你有权访问的 Azure DevOps 存储库。

   克隆完成后，Visual Studio 会打开“团队资源管理器”并显示通知。

     ![Visual Studio 2019 版本 16.7 及更低版本中，克隆完成后“团队资源管理器”窗口的屏幕截图。](./media/vs-2019/clone-complete-azure-devops.png)

1. 若要查看文件夹和文件，请选择“显示文件夹视图”链接。

     ![Visual Studio 2019 版本 16.7 及更低版本中，克隆完成后“团队资源管理器”窗口“解决方案”部分的屏幕截图。](./media/vs-2019/show-folder-view-azure-devops.png)

     Visual Studio 随即打开“解决方案资源管理器”。

1. 选择“解决方案和文件夹”链接，搜索要打开的解决方案文件（具体是 .sln 文件）。

      ![Visual Studio 2019 版本 16.7 及更低版本中，团队资源管理器中“解决方案和文件夹”通知的屏幕截图。](./media/open-proj-repo-solutions-folders.png)

   如果存储库中没有解决方案文件，则会显示消息“找不到解决方案”。 但是，可以双击文件夹菜单中的任意文件，以便在 Visual Studio 代码编辑器中将其打开。

::: moniker-end

::: moniker range="vs-2017"

## <a name="open-a-project-from-a-github-repo-with-visual-studio-2017"></a>使用 Visual Studio 2017 打开 GitHub 存储库中的项目

1. 打开 Visual Studio 2017。

1. 在顶部菜单栏中，选择“文件”>“打开”>“在源代码管理中打开”  。

   随即打开“团队资源管理器 - 连接”窗格。

    ![Visual Studio IDE 内的“团队资源管理器”窗口](./media/open-proj-repo-team-explorer.png)

1. 在“本地 Git 存储库”部分中，选择“克隆” 。

    ![从“本地 Git 存储库”部分中选择“克隆”](./media/open-proj-repo-local-git-repo-clone.png)

1. 在“输入要克隆的 Git 存储库的 URL”框中，键入或粘贴存储库的 URL，然后按 Enter__***。 （可能会收到登录到 GitHub 的提示；如果是这样，请按照提示操作。）

   Visual Studio 克隆存储库后，团队资源管理器将关闭，解决方案资源管理器将打开。 随即显示一条消息：“单击上面的‘解决方案和文件夹’以查看解决方案列表”。 选择“解决方案和文件夹”  。

   ![从解决方案资源管理器中选择“解决方案和文件夹”](./media/open-proj-repo-github-solutions-folders.png)

1. 如果有可用的解决方案文件，它会显示在“解决方案和文件夹”弹出菜单中。 选择它后，Visual Studio 将打开你的解决方案。

   ![选择想要从“解决方案资源管理器”下拉列表中打开的内容。](./media/open-proj-repo-github-solutions-folders-picker.png)

   如果存储库中没有解决方案文件（具体是 .sln 文件），弹出菜单会显示“未找到解决方案”。 但是，可以双击文件夹菜单中的任意文件，以便在 Visual Studio 代码编辑器中将其打开。

### <a name="review-your-work"></a>检查工作

查看以下动画以检查你在上一节中完成的工作。

   ![动画：使用 Visual Studio 2017 打开 GitHub 存储库中的项目。](./media/open-project-from-github.gif)

## <a name="open-a-project-from-an-azure-devops-repo-with-visual-studio-2017"></a>使用 Visual Studio 2017 打开 Azure DevOps 存储库中的项目

1. 打开 Visual Studio 2017。

1. 在顶部菜单栏中，选择“文件”>“打开”>“在源代码管理中打开”  。

   随即打开“团队资源管理器 - 连接”窗格。

    ![Visual Studio IDE 内的“团队资源管理器”窗口。](./media/open-proj-repo-team-explorer.png)

1. 可通过两种方式连接到 Azure DevOps 存储库：

      - 在“托管服务提供程序”部分中，选择“连接…” 。

        ![Visual Studio IDE 内的“团队资源管理器”窗口的“托管服务提供程序”部分。](./media/open-proj-repo-azure-devops.png)

      - 在“管理连接”下拉列表中，选择“连接到项目…” 。

        ![Visual Studio IDE 内的“团队资源管理器”窗口的“管理连接”部分。](./media/open-proj-repo-azuredevops-manage-connections.png)

1. 在“连接到项目”对话框中，选择要连接的存储库，然后选择“克隆” 。

      ![从 Visual Studio 生成的“连接到项目”对话框。](./media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > 列表框中显示的内容取决于你有权访问的 Azure DevOps 存储库。

1. Visual Studio 克隆存储库后，团队资源管理器将关闭，解决方案资源管理器将打开。 随即显示一条消息：“单击上面的‘解决方案和文件夹’以查看解决方案列表”。 选择“解决方案和文件夹”。

      ![Visual Studio 的团队资源管理器中的“解决方案和文件夹”通知。](./media/open-proj-repo-solutions-folders.png)

   “解决方案和文件夹”弹出菜单中会显示一个解决方案文件（具体是 .sln 文件）。 选择它后，Visual Studio 将打开你的解决方案。

   如果存储库中没有解决方案文件，弹出菜单会显示“未找到解决方案”。 但是，可以双击文件夹菜单中的任意文件，以便在 Visual Studio 代码编辑器中将其打开。

::: moniker-end

## <a name="next-steps"></a>后续步骤

如果需要，可以深入了解以下特定于语言的任何教程：

- [Visual Studio 教程 | C#](./csharp/index.yml)
- [Visual Studio 教程 | Visual Basic](./visual-basic/index.yml)
- [Visual Studio 教程 | C++](/cpp/get-started/tutorial-console-cpp)
- [Visual Studio 教程 | Python](../python/index.yml)
- [Visual Studio 教程 | JavaScript、TypeScript 和 Node.js](../javascript/index.yml)

## <a name="see-also"></a>另请参阅

::: moniker range="<=vs-2019"

- [Visual Studio 中的 Git 体验](../version-control/git-with-visual-studio.md)
- [并行比较 Git 和团队资源管理器](../version-control/git-team-explorer-feature-comparison.md)
- [Microsoft Learn：Visual Studio 中的 Git 和 GitHub 入门](/learn/modules/visual-studio-github-push/)
- [Microsoft Learn：Azure DevOps 入门](/learn/modules/get-started-with-devops/)
- [Azure DevOps Services：Azure Repos 和 Visual Studio 入门](/azure/devops/repos/git/gitquickstart/)

::: moniker-end

::: moniker range="vs-2022"

[Visual Studio 版本控制文档](../version-control/index.yml)

::: moniker-end