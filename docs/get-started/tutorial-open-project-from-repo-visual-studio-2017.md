---
title: 教程：在 Visual Studio 2017 中打开存储库中的项目
description: 了解如何使用 Visual Studio 2017 打开 Git 或 Azure DevOps 存储库中的项目。
ms.custom: vs-acquisition, get-started
ms.date: 02/15/2021
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
monikerRange: vs-2017
ms.openlocfilehash: 5543a568f7246d9600ba375d9a1cf19af4cbd2d4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640708"
---
# <a name="tutorial-open-a-project-from-a-repo-in-visual-studio-2017"></a>教程：在 Visual Studio 2017 中打开存储库中的项目

在本教程中，你将使用 Visual Studio 2017 首次连接到存储库，然后打开其中的一个项目。

> [!TIP]
> [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) 提供了一种更完全集成的新方法来连接 GitHub 存储库。 有关详细信息，请参阅 [Visual Studio 2019 中的新 Git 体验](../ide/git-with-visual-studio.md?view=vs-2019&preserve-view=true)页面。

## <a name="open-a-project-from-a-github-repo-by-using-visual-studio-2017"></a>使用 Visual Studio 2017 打开 GitHub 存储库中的项目

1. 打开 Visual Studio 2017。

1. 在顶部菜单栏上，选择“文件” > “打开” > “在源代码管理中打开”  。

   随即打开“团队资源管理器 - 连接”窗格。

    ![Visual Studio IDE 内的“团队资源管理器”窗口](./media/open-proj-repo-team-explorer.png)

1. 在“本地 Git 存储库”部分中，选择“克隆” 。

    ![从“本地 Git 存储库”部分中选择“克隆”](./media/open-proj-repo-local-git-repo-clone.png)

1. 在“输入要克隆的 Git 存储库的 URL”框中，键入或粘贴存储库的 URL，然后按 Enter__***。 （可能会收到登录到 GitHub 的提示；如果是这样，请按照提示操作。）

   Visual Studio 克隆存储库后，团队资源管理器将关闭，解决方案资源管理器将打开。 随即显示一条消息：“单击上面的‘解决方案和文件夹’以查看解决方案列表”。 选择“解决方案和文件夹”  。

   ![从解决方案资源管理器中选择“解决方案和文件夹”](./media/open-proj-repo-github-solutions-folders.png)

1. 如果有可用的解决方案文件，它会显示在“解决方案和文件夹”弹出菜单中。 选择它后，Visual Studio 将打开你的解决方案。

   ![选择想要从“解决方案资源管理器”下拉列表中打开的解决方案](./media/open-proj-repo-github-solutions-folders-picker.png)

   如果存储库中没有解决方案文件（具体是 .sln 文件），弹出菜单会显示“未找到解决方案”。 但是，可以双击文件夹菜单中的任意文件，以便在 Visual Studio 代码编辑器中将其打开。

### <a name="review-your-work"></a>检查工作

查看以下动画以检查你在上一节中完成的工作。

   ![使用 Visual Studio 的 GitHub 存储库中打开项目的动画](./media/open-project-from-github.gif)

> [!NOTE]
> 有关特定于 Visual Studio 2019 的信息，请参阅[在 Visual Studio 2019 中打开存储库中的项目](tutorial-open-project-from-repo-visual-studio-2019.md)页面。

## <a name="open-a-project-from-an-azure-devops-repo-by-using-visual-studio-2017"></a>使用 Visual Studio 2017 打开 Azure DevOps 存储库中的项目

1. 打开 Visual Studio 2017。

1. 在顶部菜单栏上，选择“文件” > “打开” > “在源代码管理中打开”  。

   随即打开“团队资源管理器 - 连接”窗格。

    ![Visual Studio IDE 内的“团队资源管理器”窗口](./media/open-proj-repo-team-explorer.png)

1. 可通过两种方式连接到 Azure DevOps 存储库：

      - 在“托管服务提供程序”部分中，选择“连接…” 。

        ![Visual Studio IDE 内的“团队资源管理器”窗口的“托管服务提供程序”部分](./media/open-proj-repo-azure-devops.png)

      - 在“管理连接”下拉列表中，选择“连接到项目…” 。

        ![Visual Studio IDE 内的“团队资源管理器”窗口的“管理连接”部分](./media/open-proj-repo-azuredevops-manage-connections.png)

1. 在“连接到项目”对话框中，选择要连接的存储库，然后选择“克隆” 。

      ![从 Visual Studio 生成的“连接到项目”对话框](./media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > 列表框中显示的内容取决于你有权访问的 Azure DevOps 存储库。

1. Visual Studio 克隆存储库后，团队资源管理器将关闭，解决方案资源管理器将打开。 随即显示一条消息：“单击上面的‘解决方案和文件夹’以查看解决方案列表”。 选择“解决方案和文件夹”。

      ![Visual Studio 中团队资源管理器中的“解决方案和文件夹”通知](./media/open-proj-repo-solutions-folders.png)

   “解决方案和文件夹”弹出菜单中会显示一个解决方案文件（具体是 .sln 文件）。 选择它后，Visual Studio 将打开你的解决方案。

   如果存储库中没有解决方案文件，弹出菜单会显示“未找到解决方案”。 但是，可以双击文件夹菜单中的任意文件，以便在 Visual Studio 代码编辑器中将其打开。

## <a name="next-steps"></a>后续步骤

如果你已准备好使用 Visual Studio 2017 进行编码，请深入了解以下特定于语言的任何教程：

- [Visual Studio 教程 | C#](./csharp/index.yml)
- [Visual Studio 教程 | Visual Basic](./visual-basic/index.yml)
- [Visual Studio 教程 | C++](/cpp/get-started/tutorial-console-cpp)
- [Visual Studio 教程 | Python](../python/index.yml)
- [Visual Studio 教程 | JavaScript、TypeScript 和 Node.js](../javascript/index.yml)

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 2019 中打开存储库中的项目](tutorial-open-project-from-repo-visual-studio-2019.md)
- [Visual Studio 2019 中的 Git 新体验](../ide/git-with-visual-studio.md)
- [Azure DevOps Services：Azure Repos 和 Visual Studio 入门](/azure/devops/repos/git/gitquickstart/)
- [Microsoft Learn：Azure DevOps 入门](/learn/modules/get-started-with-devops/)
