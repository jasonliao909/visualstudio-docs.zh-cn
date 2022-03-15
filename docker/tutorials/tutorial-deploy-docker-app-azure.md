---
title: 教程：将 Docker 应用部署到 Azure
description: 本教程中介绍如何将 Docker 应用部署到云中。 你可以创建云上下文并在云中运行容器。
author: ucheNkadiCode
ms.author: uchen
ms.prod: vs-code
ms.topic: tutorial
ms.date: 03/04/2022
ms.custom:
- template-tutorial
- contperf-fy22q3
ms.openlocfilehash: 508593b37e2f2b5db22565796e77b1e4ceabeb5f
ms.sourcegitcommit: 5b2c3a2c5f22e0cd6d35aab6049c1f61c4916e74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2022
ms.locfileid: "139852212"
---
# <a name="tutorial-deploy-your-docker-app-to-azure"></a>教程：将 Docker 应用部署到 Azure

在本教程中，你将学习如何在云中运行容器化应用程序。
其他人可以访问并利用它。

本教程介绍如何执行下列操作：

> [!div class="checklist"]
> - 创建云上下文。
> - 在云中运行容器。

## <a name="prerequisites"></a>先决条件

本教程将继续学习上一个教程，即[使用 Visual Studio Code 创建和共享 Docker 应用](docker-tutorial.md)。
从该教程开始，其中包括先决条件。
然后学习此教程：[永久保存数据和层 Docker 应用](tutorial-persist-data-layer-docker-app-with-vscode.md)。

对于本教程，还需要以下各项：

- 具有活动订阅的 Azure 帐户。
  [免费创建帐户](https://azure.microsoft.com/free/)。
- 适用于 VS Code 的 Azure 帐户扩展。
  若要安装它，请选择 VS Code 的左侧栏中的“扩展”图标，然后搜索“Azure 帐户”。

## <a name="create-your-cloud-context"></a>创建云上下文

若要将应用部署到云中，请使用 Docker 上下文。
上下文是指当前正在使用容器的位置。
现在，只有默认上下文。

需要创建 Azure 容器实例 (ACI) 上下文。
此过程创建上下文。

1. 在 VS Code 中，通过查看 Docker 视图的“上下文”部分来查看已有的上下文。

   ![屏幕截图显示 Docker 扩展的“上下文”区域，其中只包含默认上下文。](media/default-context.png)

   应该只能看到本地工作的默认上下文。

1. 选择“查看” > “命令面板”   。 输入“Docker 上下文: 创建 Azure 容器实例上下文”。

   如果尚未登录 Azure，VS Code 会发出提示。

1. 输入上下文的名称。

   ![屏幕截图显示新上下文的名称条目。](media/create-new-context.png)

1. 输入要使用的资源组。
   可以改为创建资源组。

   ![屏幕截图显示用于选择或创建资源组的选项。](media/select-resource-group.png)

   ACI 上下文现在显示在“上下文”下。 选择它作为当前使用的上下文。

   ![屏幕截图显示 Docker 扩展上下文，其中添加了新上下文。](media/list-contexts.png)

## <a name="run-containers-in-the-cloud"></a>在云中运行容器

在 Azure 中创建上下文后，可以在云中运行容器。

1. 运行以下命令。

   ```bash
   docker context use newacicontext
   docker run  -dp 3000:3000 <username>/getting-started
   ```

1. 在 Docker 视图的“容器”下，检查容器是否正在运行。

   ![屏幕截图显示 Docker 扩展中的容器。](media/context-container.png)

1. 若要检查容器是否正常运行，请右键单击正在运行的容器，然后选择“在浏览器中打开”。

   ![屏幕截图再次显示示例应用，这一次是从 Azure 容器实例容器启动的。](media/container-instance.png)

   容器正在使用公共 IP 地址运行并且工作正常。

1. 查看正在运行的容器，以查看其工作方式。
   可以首先查看容器日志：

   ```bash
   docker logs <container-name>
   ```

   在“getting-started”旁的“容器”下获取容器名称 

1. 可以在容器中使用 `docker exec` 命令，就像在本地容器中一样。

   ```bash
   docker exec -it container-name sh
   ```

1. 若要清理工作空间并确保不会因继续运行测试容器而产生任何费用，右键单击正在运行的容器，然后选择“移除”。

## <a name="clean-up-resources"></a>清理资源

保留迄今为止所完成的一切内容，以继续学习下面的其他教程。

你在本系列教程中使用的先决条件可用于未来的 Docker 开发。
除了添加到 Azure 的测试容器，无需删除或卸载任何内容。

## <a name="next-steps"></a>后续步骤

你已完成该系列教程。
在本教程中，你已创建了工作负载并已成功将其部署到云中。

下面是使用容器时可以采用的其他路径。

- 容器业务流程

  Kubernetes、Swarm、Nomad 和 Azure Kubernetes Service (AKS) 等工具都可解决在生产环境中运行容器所面临的问题。

  通常，你会设置“管理员”来接收“预期状态” 。
  然后，管理员会查看群集中的计算机，并将工作委托给工作器节点。
  管理员查看更改（如容器退出），然后进行处理以使“实际状态”反映预期状态。

- 云原生计算基础项目

  云原生计算基础 (CNCF) 独立于供应商，适合各种开放源代码项目，包括 Kubernetes、Prometheus、Envoy 和 Linkerd。
  可以查看[成熟和孵化项目](https://www.cncf.io/projects/)，以及整个 [CNCF 云原生交互环境](https://landscape.cncf.io/)。
  有一些项目可帮助解决监视、日志记录、安全性、映像注册表和消息传递问题。

了解有关使用 VS Code Docker 扩展的详细信息：

- [VS Code Docker 扩展概述](https://code.visualstudio.com/docs/containers/overview)
- [Node.js 入门](https://code.visualstudio.com/docs/containers/quickstart-node)
- [Python 入门](https://code.visualstudio.com/docs/containers/quickstart-python)
- [.NET Core 入门](https://code.visualstudio.com/docs/containers/quickstart-aspnet-core)
- [调试容器化应用](https://code.visualstudio.com/docs/containers/debug-common)

你可能对此基于当前教程系列的可选教程感兴趣：

> [!div class="nextstepaction"]
> [创建具有 MySQL 和 Docker Compose 的多容器应用](tutorial-multi-container-app-mysql.md)
