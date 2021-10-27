---
title: 连接到团队资源管理器中的项目
description: 了解如何使用 Visual Studio 中的团队资源管理器，与团队成员一起开发和管理项目。
ms.custom: SEO-VS-2020
ms.date: 06/11/2021
ms.topic: conceptual
ms.author: tglee
author: TerryGLee
ms.manager: jmartens
monikerRange: <=vs-2019
ms.openlocfilehash: fd95da37fc0f6dcf5d7c735bc1e8b1afe050b9f8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641208"
---
# <a name="connect-to-projects-in-team-explorer"></a>连接到团队资源管理器中的项目

::: moniker range="vs-2017"

使用“团队资源管理器”工具窗口与其他团队成员协调代码工作，以开发项目，并管理分配给你、你的团队或项目的工作。 团队资源管理器将 Visual Studio 连接到 Git 和 GitHub 存储库、Team Foundation 版本控制 (TFVC) 存储库以及 [Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) 或本地 [Azure DevOps Server](/azure/devops/index-all)（以前称为 TFS）上托管的项目。 你可管理源代码、工作项和生成。

::: moniker-end

::: moniker range="vs-2019"

团队资源管理器将 Visual Studio 连接到 Team Foundation 版本控制 (TFVC) 存储库以及 [Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) 或本地 [Azure DevOps Server](/azure/devops/user-guide/about-azure-devops-services-tfs?view=azure-devops&preserve-view=true)（以前称为 TFS）上托管的项目。 你可管理源代码、工作项和生成。

> [!IMPORTANT]
> 在 Visual Studio 2019 [版本 16.8](/visualstudio/releases/2019/release-notes-history) 中，默认启用 Git 版本控制体验。 若要详细了解它如何与团队资源管理器进行比较，请参阅 [Git 和团队资源管理器的并行比较](../version-control/git-team-explorer-feature-comparison.md)页。
>
> 不过，如果更希望继续使用团队资源管理器，则转到“工具”>“选项”>“环境”>“预览功能”，然后切换“新的 Git 用户体验”复选框。

使用团队资源管理器连接到项目的方式取决于你使用的 Visual Studio 2019 的版本。

## <a name="in-version-168-and-later"></a>在版本 16.8 及更高版本中

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

## <a name="in-version-167-and-earlier"></a>在版本 16.7 及更低版本中

1. 打开 Visual Studio 2019。

1. 在起始窗口上，选择“克隆或签出代码”。

   ![Visual Studio 2019 版本 16.7 及更低版本中“新建项目”窗口的屏幕截图](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. 在“浏览存储库”部分中，选择“Azure DevOps” 。

   ![Visual Studio 2019 版本 16.7 及更低版本中“克隆或签出代码”窗口的屏幕截图，其中“浏览存储库”部分列出了 Azure DevOps](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   如果看到登录窗口，请登录帐户。

1. 在“连接到项目”对话框中，选择要连接的存储库，然后选择“克隆” 。

      ![从 Visual Studio 2019 版本 16.7 及更低版本生成的“连接到项目”对话框的屏幕截图](../get-started/media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > 列表框中显示的内容取决于你有权访问的 Azure DevOps 存储库。

   克隆完成后，Visual Studio 会打开“团队资源管理器”并显示通知。

     ![Visual Studio 2019 版本 16.7 及更低版本中，克隆完成后“团队资源管理器”窗口的屏幕截图](../get-started/media/vs-2019/clone-complete-azure-devops.png)

1. 若要查看文件夹和文件，请选择“显示文件夹视图”链接。

     ![Visual Studio 2019 版本 16.7 及更低版本中，克隆完成后“团队资源管理器”窗口“解决方案”部分的屏幕截图](../get-started/media/vs-2019/show-folder-view-azure-devops.png)

     Visual Studio 随即打开“解决方案资源管理器”。

1. 选择“解决方案和文件夹”链接，搜索要打开的解决方案文件（具体是 .sln 文件）。

      ![Visual Studio 2019 版本 16.7 及更低版本中，团队资源管理器中“解决方案和文件夹”通知的屏幕截图](../get-started/media/open-proj-repo-solutions-folders.png)

   如果存储库中没有解决方案文件，则会显示消息“找不到解决方案”。 但是，可以双击文件夹菜单中的任意文件，以便在 Visual Studio 代码编辑器中将其打开。

::: moniker-end

::: moniker range="vs-2017&quot;

![Visual Studio 中的团队资源管理器主页](media/team-explorer/team-explorer.png &quot;Visual Studio 中的团队资源管理器主页。")

> [!TIP]
> 如果打开 Visual Studio 但未显示团队资源管理器，请从菜单栏中选择“视图” > “团队资源管理器”将其打开，或者通过按“Ctrl+\”和“Ctrl+M”      。

## <a name="connect-to-a-project-or-repository"></a>连接到项目或存储库

连接到“连接”页上的项目或存储库。

![团队资源管理器中的“连接”页](media/team-explorer/connect.png "Visual Studio 中的团队资源管理器“连接”页面")

要连接到项目：

1. 选择“管理连接”图标，打开“连接”页 。

   ![团队资源管理器中的“管理连接”按钮](media/team-explorer/manage-connections.png "Visual Studio 中的团队资源管理器“管理连接”按钮。")

1. 在“连接”页上，选择“管理连接”>“连接到项目”。

   ![连接到团队资源管理器中的项目](media/team-explorer/connect-project.png "Visual Studio 中的团队资源管理器“连接到项目”页面。")

> [!TIP]
> 如果要打开存储库中的项目，请参阅[打开存储库中的项目](../get-started/tutorial-open-project-from-repo-visual-studio-2017.md)。 如果要创建新项目或将用户添加到项目，请参阅[创建项目 (Azure DevOps)](/azure/devops/organizations/projects/create-project) 和[将用户添加到项目或团队 (Azure DevOps)](/azure/devops/organizations/security/add-users-team-project)。

::: moniker-end

## <a name="see-also"></a>请参阅

- [并行比较 Git 和团队资源管理器](git-team-explorer-feature-comparison.md)
- [Visual Studio 中的 Git 新体验](git-with-visual-studio.md)
- [团队资源管理器参考](reference/team-explorer-reference.md)
- [连接到项目 (Azure DevOps)](/azure/devops/organizations/projects/connect-to-projects)
- [排查项目连接问题](/azure/devops/user-guide/troubleshoot-connection?view=azure-devops&preserve-view=true)
