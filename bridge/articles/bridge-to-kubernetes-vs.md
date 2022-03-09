---
title: 教程：在本地运行和调试，Bridge to Kubernetes本地Visual Studio
description: 在本教程中，了解如何将 Bridge to Kubernetes 与 Visual Studio 连接到群集，并使用本地隧道调试来调试 Kubernetes 服务。
keywords: Bridge to Kubernetes, Azure Dev Spaces, Dev Spaces, Docker, Kubernetes, Azure, 容器
ms.author: ghogen
author: ghogen
manager: jmartens
ms.technology: bridge
ms.custom: contperf-fy22q1
ms.topic: tutorial
ms.date: 02/22/2022
ms.openlocfilehash: 4366b53869e1cf74ac5058f498aa8ebf12f6b12f
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139549199"
---
# <a name="tutorial-run-and-debug-locally-with-bridge-to-kubernetes-on-visual-studio"></a>教程：在本地运行和调试，Bridge to Kubernetes本地Visual Studio

本教程介绍如何在 Kubernetes 群集与开发计算机之间重定向流量。
本教程使用 Bridge to Kubernetes 和 Visual Studio 调试服务。
若要使用Visual Studio Code，请参阅使用 Bridge to Kubernetes [本地VS Code](bridge-to-kubernetes-vs-code.md)。

若要详细了解Bridge to Kubernetes，请参阅Bridge to Kubernetes [工作原理](overview-bridge-to-kubernetes.md)。

在本教程中，你将了解如何执行以下操作：

> [!div class="checklist"]
> - 连接群集的 Bridge to Kubernetes。
> - 出于开发目的，将请求路由到本地运行的服务。
> - 在本地计算机上调试正在运行的服务。

## <a name="prerequisites"></a>先决条件

- 一个 Kubernetes 群集。 可以在"创建"[中Azure 门户。](https://azure.microsoft.com/free/)  如果没有 Azure 订阅，可以[免费创建一个帐户](https://azure.microsoft.com/free/)。
- [系统上安装的 kubectl](https://kubernetes.io/docs/reference/kubectl/kubectl/) 可执行文件。
- [Visual Studio 2019](https://www.visualstudio.com/vs/) 版本 16.7 或更高版本，Windows 10或更高版本。
- Bridge to Kubernetes[的 Visual Studio](https://aka.ms/bridge-to-k8s-vsc-extension)。
- 要故障排除的应用程序，例如此 [TODO 应用示例应用程序](https://github.com/Microsoft/mindaro)。

## <a name="set-up-a-service"></a>设置服务

本教程使用 Bridge to Kubernetes在任何 Kubernetes 群集上处理简单的 todo 示例应用程序。

示例应用程序有一个要交互的前端和一个提供持久存储的后端。

1. 打开 Bash 窗口，检查群集是否可用并准备就绪。
   然后将上下文设置为该群集。

   ```bash
   kubectl cluster-info
   kubectl config use-context <kubernetes-cluster>
   ```

1. 克隆示例存储库。

   ```bash
   git clone https://github.com/Microsoft/mindaro
   ```

1. 将目录更改为 *samples/todo-app* ，然后为示例创建命名空间。

   ```cmd
   kubectl create namespace todo-app
   ```

1. 应用部署清单：

   ```cmd
   kubectl apply -n todo-app -f deployment.yaml
   ```

   此简单部署使用 类型的服务公开前端 `LoadBalancer`。
   等待所有 pod 都处于运行状态，以及 `frontend` 服务的外部 IP变为可用。

   如果使用 MiniKube 进行测试，请使用 `minikube tunnel` 解析外部 IP。
   如果你使用 AKS 或其他基于云的 Kubernetes 提供程序，系统会自动分配一个外部 IP。

1. 使用以下命令监视 `frontend` 服务，等待其启动并运行：

   ```output
   kubectl get service -n todo-app frontend --watch

   NAME       TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)        AGE
   frontend   LoadBalancer   10.0.245.78   10.73.226.228   80:31910/TCP   6m26s
   ```

## <a name="connect-to-your-cluster"></a>连接到群集

1. 打开 Visual Studio。 在" **入门"窗口中，** 选择" **继续而不编写代码"**。

1. 选择 **"Project** > **/解决方案**"，找到 *samples\todo-app\database-api\databaseApi.csproj* 项目，然后选择"打开 **"**。

1. 在项目中 **，从Bridge to Kubernetes** 设置中选择一个，如下所示：

   ![屏幕截图显示了已选择Bridge to Kubernetes工具。](media/bridge-to-kubernetes-vs/select-debug-tool.png)

1. 选择"开始" **按钮旁边的Bridge to Kubernetes**。
   在" **创建配置文件Bridge to Kubernetes** 对话框中，输入以下值：

   - 选择你的群集名称。
   - 选择“todo-app”作为命名空间。
   - 选择要 *重定向的服务***的数据库** API。
   - 选择之前用于启动浏览器的同一 URL。

   ![屏幕截图显示了"为Bridge to Kubernetes配置文件"对话框，并输入了值。](media/bridge-to-kubernetes-vs/configure-bridge-debugging.png)

1. 如果要独立运行，请选择" **启用路由隔离"**。
   如果启用路由隔离，则使用该群集的其他人不受更改的影响。
   隔离模式将请求路由到每个受影响的服务的副本。
   它正常路由其他流量。
   有关详细信息，请参阅如何 [Bridge to Kubernetes工作](overview-bridge-to-kubernetes.md#using-routing-capabilities-for-developing-in-isolation)。

1. 选择 **"保存并调试** "以保存更改。

   ![屏幕截图显示了调试中显示的 todo 服务，以及任务的输入框。](media/bridge-to-kubernetes-vs/todos-service.png)

   > [!NOTE]
   > EndpointManager 会提示你允许提升的主机 *文件* 权限。

   开发计算机连接到群集。
   状态栏显示已连接到服务 `database-api` 。

   ![屏幕截图显示了验证开发计算机已连接的状态栏。](media/bridge-to-kubernetes-vs/development-computer-connected.png)

1. 尝试输入任务，将其标记为完成。

1. 选择 **"调试** > **""停止调试** "以停止调试。
   此操作的快捷方式是 **ShiftF5** + 或使用工具栏中的"停止 **调试**"按钮。

Bridge to Kubernetes重定向数据库 *API 服务的所有* 流量。
它会重定向到开发计算机上应用程序的版本。
Bridge to Kubernetes 还会将应用程序的所有出站流量路由回 Kubernetes 群集。

> [!NOTE]
> 默认情况下，停止调试任务也会断开开发计算机与 Kubernetes 群集的连接。
> 若要更改此行为，请选择" **工具** > **""选项"**，然后选择" **Kubernetes 调试工具"**。
> 将 **"调试后断开连接"设置为** **False**。
>
>![屏幕截图显示了 Kubernetes 调试工具中的"调试后断开连接"值。](media/bridge-to-kubernetes-vs/kubernetes-debugging-options.png)
>
> 更新此设置后，当你停止并开始调试时，开发计算机将保持连接状态。
> 若要断开开发计算机与群集的连接，请单击工具栏 **上的** "断开连接"按钮。

## <a name="set-a-breakpoint"></a>设置断点

在本部分，你将在服务中设置断点。

1. 在 **解决方案资源管理器** 中，选择 **"MongoHelper.cs** "以在编辑器中打开文件。
   如果看不到"视图解决方案资源管理器， **请选择"查看** > **解决方案资源管理器"**。

1. 在 **CreateTask** 方法主体的第一行上设置光标。
   然后选择" **调试** > **""调试断点** "以设置断点。 

   ![屏幕截图显示了 CreateTask 方法，第一行中设置了断点。](media/bridge-to-kubernetes-vs/set-breakpoint.png)

   此操作的快捷方式是 **F9**。

1. 像上一 **部分Bridge to Kubernetes一** 样，选择"开始"按钮。
   调试从之前输入的值开始。

1. 在打开的浏览器中，在 **todos** 中输入值，然后选择 **Enter**。
   代码将到达你输入的断点。
   执行实际调试任务时，可以使用调试选项逐步执行代码。

1. 选择 **"调试** > **""停止调试** "以停止调试。

1. 若要删除断点，请选择该行，然后选择" **调试** > **""对断点** "或" **F9"**。

## <a name="clean-up-resources"></a>清理资源

如果在本教程中使用了示例 todo 应用，可以使用以下方法将其从群集Azure 门户。
如果在本地克隆了该存储库，可以手动将其删除。

## <a name="next-steps"></a>后续步骤

若要详细了解 Bridge to Kubernetes，请参阅 [Bridge to Kubernetes 工作原理](overview-bridge-to-kubernetes.md)。

有关支持的功能和路线图的信息，请参阅Bridge to Kubernetes路线图Bridge to Kubernetes [路线图](https://github.com/microsoft/mindaro/projects/1)。

若要了解如何使用 Visual Studio Code 将开发计算机连接到群集，请查看此文：
> [!div class="nextstepaction"]
> [使用 Bridge to Kubernetes (VS Code)](bridge-to-kubernetes-vs-code.md)
