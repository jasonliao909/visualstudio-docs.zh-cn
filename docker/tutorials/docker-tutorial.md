---
title: 教程： Visual Studio Code 中的 Docker 应用入门
description: 在本教程中，了解如何开始使用 Docker 与 VS Code。 创建应用并将其部署到 Azure。
author: ucheNkadiCode
ms.author: uchen
ms.prod: vs-code
ms.topic: tutorial
ms.date: 03/04/2022
ms.custom: template-tutorial
ms.openlocfilehash: db7e0e5add9f98c4b51d7835236c4deb3001165e
ms.sourcegitcommit: 71f68518d53d29e892934863ce10ceaa7613a966
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139608425"
---
# <a name="tutorial-create-and-share-a-docker-app-with-visual-studio-code"></a>教程：使用 Visual Studio Code 创建和共享 Docker 应用

本教程是一个由三个部分组成的系列教程，介绍如何使用 Visual Studio Code (VS Code) 引入 Docker。
你将了解如何创建和运行容器、保存数据以及将容器化应用程序部署到 Azure。

在第一个教程中，你将学习如何创建和部署 Docker 应用。
然后，可以更新并共享容器化应用。

容器是精简虚拟化的环境，如虚拟机，它提供用于生成和运行应用程序的平台。
容器不需要完整操作系统的大小和开销。
[Docker](https://www.docker.com) 是一个行业标准的第三方容器提供程序和容器管理系统。

Docker Desktop 在您的计算机上运行，并管理您的本地容器。
开发工具（如 Visual Studio 和 VS Code 提供可让你使用本地 Docker 桌面服务的扩展。
可以创建容器化应用，将应用部署到容器，并调试容器上运行的应用。

在本教程中，你将了解如何执行以下操作：

> [!div class="checklist"]
> - 创建容器。
> - 生成容器映像。
> - 启动应用容器。
> - 更新代码并替换容器。
> - 共享映像。
> - 在新的实例上运行映像。

## <a name="prerequisites"></a>先决条件

- [Visual Studio Code](https://code.visualstudio.com/download)。
- [Docker VS Code 扩展](https://code.visualstudio.com/docs/containers/overview)。
- [Docker Desktop](https://docs.docker.com/desktop/)。
- [Docker 中心](https://hub.docker.com/signup)帐户。 可以免费创建帐户。

## <a name="create-a-container"></a>创建容器

容器是计算机上的进程。
它与主计算机上的所有其他进程隔离。
该隔离使用内核命名空间和控制组。

容器使用独立的文件系统。
此自定义文件系统由一个容器映像提供。
映像包含运行应用程序所需的所有内容，例如所有依赖项、配置、脚本和二进制文件。
映像还包含容器的其他配置，例如环境变量、要运行的默认命令以及其他元数据。

安装适用于 VS Code 的 Docker 扩展后，可以使用 VS Code 中的容器。
除了 Docker 窗格中的上下文菜单之外，还可以选择 "**终端**  >  **新终端**" 打开命令行窗口。
你还可以在 Bash 窗口中运行命令。
除非指定，否则标记为 **Bash** 的任何命令都可以在 Bash 窗口或 VS Code 终端中运行。

1. 在 VS Code 中，选择 **终端**  >  **新终端**。

1. 在终端窗口或 Bash 窗口中运行以下命令。

   ```bash
   docker run -d -p 80:80 docker/getting-started
   ```

   此命令包含以下参数：

   - `-d` 在后台以分离模式运行容器。
   - `-p 80:80` 将主机的端口80映射到容器中的端口80。
   - `docker/getting-started` 指定要使用的映像。

   > [!TIP]
   > 可以组合单字符标志以缩短整个命令。
   > 例如，可将上述命令编写为：
   >
   > ```bash
   > docker run -dp 80:80 docker/getting-started
   > ```

1. 在 VS Code 中，选择左侧的 docker 图标以查看 docker 扩展。

   ![屏幕截图显示 docker 扩展，其中运行了 docker/入门教程。](media/vs-tutorial-docker-extension.png)

   Docker VS Code 扩展显示在计算机上运行的容器。
   可以访问容器日志和管理容器生命周期，如 "停止" 和 "删除"。

   在此示例中，将随机创建容器名称， **modest_schockly** 。
   你的名称将使用不同的名称。

1. 右键单击 " **docker/** 入门" 以打开上下文菜单。
   选择“在浏览器中打开”。

   相反，请打开浏览器并输入 `http://localhost/tutorial/` 。

   你将看到一个本地托管的页面，其中大约为 DockerLabs。

1. 右键单击 " **docker/** 入门" 以打开上下文菜单。
   选择 " **删除** " 以删除此容器。

   若要使用命令行删除容器，请运行以下命令获取其容器 ID：

   ```bash
   docker ps
   ```

   然后停止并删除容器：

   ```bash
   docker stop <container-id>
   docker rm <container-id>
   ```

1. 刷新浏览器。
   现在，您看到的入门页面已消失。

## <a name="build-a-container-image-for-the-app"></a>为应用程序构建容器映像

本教程使用一个简单的 Todo 应用程序。

![屏幕截图显示添加了多个项的示例应用程序和一个用于添加新项的文本框和按钮。](media/todo-list-sample.png)

应用允许你创建工作项并将其标记为 "已完成" 或 "删除"。

为了生成应用程序，请创建一个 *Dockerfile*。
Dockerfile 是一种基于文本的说明脚本，用于创建容器映像。

1. 请参阅 [Docker 入门教程](https://github.com/docker/getting-started)存储库，然后选择 "**代码**  >  " "**下载 ZIP**"。
   将内容提取到本地文件夹。

   ![屏幕截图显示 Github 站点的一部分，其中突出显示了 "绿色代码" 按钮和 "下载 ZIP" 选项。](media/download-zip.png)

1. 在 VS Code 中，选择 "**文件**  >  " "**打开文件夹**"。
   导航到所提取项目中的 *应用* 文件夹，然后打开该文件夹。
   应该会看到一个名为 *package* 的文件和两个名为 *src* 和 *spec* 的文件夹。

   ![显示 package 文件的屏幕 Visual Studio Code 截图，其中加载了应用程序。](media/ide-screenshot.png)

1. 使用以下内容，在与文件 *包* 相同的文件夹中创建名为 *Dockerfile* 的文件。

   ```dockerfile
   FROM node:12-alpine
   WORKDIR /app
   COPY . .
   RUN yarn install --production
   CMD ["node", "/app/src/index.js"]
   ```

   > [!NOTE]
   > 确保该文件没有文件扩展名，例如 `.txt` 。

1. 在文件资源管理器的 VS Code 中，右键单击 *Dockerfile* ，然后选择 "**生成映像**"。
   在文本输入框中输入 " *入门* " 作为图像的标记。

   标记为图像的友好名称。

   若要从命令行创建容器映像，请使用以下命令。

    ```bash
    docker build -t getting-started .
    ```

    > [!NOTE]
    > 在 "外部 Bash" 窗口中，打开 `app` 包含 *Dockerfile* 的文件夹以运行此命令。

你已使用 *Dockerfile* 生成新的容器映像。
您可能已注意到许多 "层" 已下载。
*Dockerfile* 从 `node:12-alpine` 映像开始。
除非你的计算机上已存在，否则需要下载该映像。

下载映像后， *Dockerfile* 将复制应用程序，并使用 `yarn` 来安装应用程序的依赖项。
*Dockerfile* 中的 `CMD` 值指定从此映像启动容器时要运行的默认命令。

命令末尾 `docker build` 处的 `.` 指示 Docker 应该在当前目录中查找 *Dockerfile* 。

## <a name="start-your-app-container"></a>启动应用容器

现在，你已有了一个映像，接下来可以运行该应用程序。

1. 若要启动容器，请使用以下命令。

   ```bash
   docker run -dp 3000:3000 getting-started
   ```

   `-d`参数指示在后台运行处于分离模式的容器。
   `-p`该值会在主机端口3000和容器端口3000之间创建映射。
   如果没有端口映射，你将无法访问应用程序。

1. 几秒钟后，在 "VS Code 的" Docker "区域中的"**容器**"下，右键单击"**入门**"，然后选择"**在浏览器中打开**"。
   您可以改为 `http://localhost:3000` 打开 web 浏览器。

   应会看到应用正在运行。

   ![屏幕截图显示没有任何项的示例应用程序，但未添加上述项的文本。](media/todo-list-empty.png)

1. 添加一项或两项，看看它按预期工作。
   可以将项标记为完成项和删除项。
   前端已成功地将项存储在后端中。

## <a name="update-the-code-and-replace-the-container"></a>更新代码并替换容器

此时，您有一个正在运行的待办事项列表管理器，其中包含几个项。
现在，让我们做一些更改，并了解如何管理容器。

1. `src/static/js/app.js`在文件中，将第56行更新为使用这个新的文本标签：

   ```diff
   - <p className="text-center">No items yet! Add one above!</p>
   + <p className="text-center">You have no todo items yet! Add one above!</p>
   ```

    保存所做更改。

1. 停止并删除容器的当前版本。
   多个包含不能使用同一个端口。

   右键单击 " **入门** " 容器，然后选择 " **删除**"。

   ![屏幕截图显示 Docker 扩展，其中已选择容器，并显示带有删除选项的上下文菜单。](media/vs-remove-container.png)

   或者，从命令行使用以下命令获取容器 ID。

   ```bash
   docker ps
   ```

   然后停止并删除容器：

   ```bash
   docker stop <container-id>
   docker rm <container-id>
   ```

1. 生成映像的更新版本。
   在文件资源管理器中，右键单击 *Dockerfile*，然后选择 " **生成映像**"。

   或者，若要在命令行上生成，请使用之前使用的相同命令。

    ```bash
    docker build -t getting-started .
    ```

1. 启动一个使用更新的代码的新容器。

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

1. 刷新浏览器 `http://localhost:3000` 以查看更新的帮助文本。

   ![屏幕截图显示带有修改后的文本的示例应用程序，如上所述。](media/todo-list-updated-empty-text.png)

## <a name="share-your-image"></a>共享映像

构建映像后，可以将其共享。
若要共享 Docker 映像，请使用 Docker 注册表。
默认注册表为 Docker Hub，其中使用的所有映像均来自。

要推送映像，首先需要在 Docker Hub 上创建存储库。

1. 请中转到 [Docker Hub](https://hub.docker.com) 并登录到你的帐户。

1. 选择 " **创建存储库**"。

1. 对于 "存储库名称"，请输入 `getting-started` 。
   请确保 **可见性** 是 **公共** 的。

1. 选择“创建”。

   在页面右侧，会看到一个名为 **Docker 命令** 的部分。
   本部分提供运行以推送到此存储库的示例命令。

   ![屏幕截图使用建议的 Docker 命令显示 Docker 中心页。](media/push-command.png)

1. 在 VS Code 的 Docker 视图的 "**图像**" 下，右键单击图像标记，然后选择 "**推送**"。
   选择 **连接注册表**，然后选择 **Docker 中心**。

   需要输入 Docker 中心帐户、密码和命名空间。

若要使用命令行推送到 Docker 中心，请使用此过程。

1. 登录到 Docker 中心：

   ```bash
   docker login -u <username>
   ```

1. 使用以下命令为 *入门* 映像指定一个新名称。

    ```bash
    docker tag getting-started <username>/getting-started
    ```

1. 使用以下命令推送容器。

    ```bash
    docker push <username>/getting-started
    ```

## <a name="run-the-image-on-a-new-instance"></a>在新的实例上运行映像

既然已生成映像并将其推送到注册表中，请尝试在从未见过此容器映像的全新实例上运行该应用。
若要运行应用，请使用 Docker。

1. 打开浏览器，转到 [Play with Docker](http://play-with-docker.com)。

1. 使用 Docker Hub 帐户登录。

1. 选择 " **启动** "，然后选择左侧栏中的 " **+ 添加新实例** " 链接。
   几秒钟后，浏览器中将打开一个终端窗口。

   ![屏幕截图显示使用 "添加新实例" 链接播放 Docker 网站。](media/play-with-docker-add-new-instance.png)

1. 在终端中，启动应用。

    ```bash
    docker run -dp 3000:3000 <username>/getting-started
    ```

    通过 Docker 播放映像并启动映像。

1. 选择 "**打开端口**" 旁边的 **3000** 徽章。
   你应看到该应用进行了修改。

   如果未显示 **3000** 徽章，请选择 " **打开端口** "，然后输入3000。

## <a name="clean-up-resources"></a>清理资源

请随时完成此系列教程中的所有操作。

## <a name="next-steps"></a>后续步骤

你已完成本教程。
已了解如何创建容器映像，运行容器化应用程序，更新代码，并在新实例上运行映像。

下面是一些可能对你有用的资源：

- [Docker 云集成](https://github.com/docker/compose-cli)
- [示例](https://github.com/docker/awesome-compose)

接下来，请尝试学习本系列教程中的下一个教程：

> [!div class="nextstepaction"]
> [持久保存数据和将 Docker 应用分层](tutorial-persist-data-layer-docker-app-with-vscode.md)
