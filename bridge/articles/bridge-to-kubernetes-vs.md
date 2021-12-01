---
title: 教程：使用 Bridge to Kubernetes 连接开发计算机
ms.technology: bridge
ms.custom: contperf-fy22q1
ms.date: 03/24/2021
ms.topic: tutorial
description: 在 Visual Studio 中使用 Bridge to Kubernetes 将开发计算机连接到 Kubernetes 群集。
keywords: Bridge to Kubernetes, Azure Dev Spaces, Dev Spaces, Docker, Kubernetes, Azure, 容器
ms.author: ghogen
author: ghogen
manager: jmartens
ms.openlocfilehash: 2be3c39f98b4127bf27801797beea35a1ec9f29f
ms.sourcegitcommit: d63ba1eff845d41ca095efb14b499ea96c4b6eba
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2021
ms.locfileid: "129560965"
---
# <a name="use-bridge-to-kubernetes-visual-studio"></a>使用 Bridge to Kubernetes (Visual Studio)

在本教程中，你将了解如何使用 Bridge to Kubernetes 来重定向 Kubernetes 群集与开发计算机上运行的代码之间的流量。 

本指南还提供了一个脚本，用于在 Kubernetes 群集上部署包含多个微服务的大型示例应用程序。

若要详细了解 Bridge to Kubernetes，请参阅 [Bridge to Kubernetes 的工作原理](overview-bridge-to-kubernetes.md)一文。

## <a name="prerequisites"></a>先决条件

- 一个 Kubernetes 群集
- 在 Windows 10 或更高版本上运行的 [Visual Studio 2019][visual-studio] 版本 16.7 预览版 4 或更高版本。
- [已安装 Bridge to Kubernetes 扩展][btk-extension]

## <a name="about-the-data"></a>关于数据

本教程使用 Bridge to Kubernetes 在任何 Kubernetes 群集上开发简单的 TODO 示例应用程序的微服务版本。 这个使用 Visual Studio 的 [TODO 应用示例应用程序](http://todomvc.com)由 [TodoMVC][todo-app-github] 提供的代码改编而来。 

 这些步骤应适用于任何 Kubernetes 群集。 因此，如果你已在 Kubernetes 群集上运行自己的应用程序，仍可以执行以下步骤，使用你自己的服务名称。

TODO 应用程序示例由提供持久存储的前端和后端组成。 此扩展示例添加了一个统计信息组件，并将应用程序分解为多个微服务，具体如下：

- 前端调用 database-api 来保留和更新 TODO 项；
- database-api 服务依赖于 Mongo 数据库来保留 TODO 项；
- 前端将添加、完成和删除事件写入 RabbitMQ 队列；
- 统计信息工作者从 RabbitMQ 队列接收事件，并更新 Redis 缓存；
- 统计信息 API 公开缓存的统计数据供前端显示。

总之，此扩展 TODO 应用程序由六个相关组件组成。


## <a name="check-the-cluster"></a>检查群集

打开命令提示符，检查是否已安装 `kubectl`，以及你要使用的群集是否在路径上可用且就绪，并将上下文设置为该群集。

```cmd
kubectl cluster-info
kubectl config use-context {context-name}
```

其中，{context-name} 是要用于 todo-app 示例的群集上下文的名称。

## <a name="deploy-the-application"></a>部署应用程序

克隆 [mindaro 存储库](https://github.com/Microsoft/mindaro)，并打开一个命令窗口，其中当前工作文件夹指向 samples/todo-app。

为示例创建命名空间。

```cmd
kubectl create namespace todo-app
```

然后，应用部署清单：

```cmd
kubectl apply -n todo-app -f deployment.yaml
```

这是一个简单的部署，它使用 `LoadBalancer` 类型的服务公开前端。 等待所有 pod 都处于运行状态，以及 `frontend` 服务的外部 IP变为可用。

如果要使用 MiniKube 进行测试，则需要使用 `minikube tunnel` 解析外部 IP。 如果你使用 AKS 或其他基于云的 Kubernetes 提供程序，系统会自动分配一个外部 IP。 使用以下命令监视 `frontend` 服务，等待其启动并运行：

```output
kubectl get service -n todo-app frontend --watch

NAME       TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)        AGE
frontend   LoadBalancer   10.0.245.78   20.73.226.228   80:31910/TCP   6m26s
```

使用外部 IP 和本地端口（“端口”列中的第一个数字）浏览到应用程序。

```
http://{external-ip}:{local-port}
```

在浏览器中测试正在运行的应用。 在添加、完成和删除 todo 项时，请注意，统计信息页将以预期的指标进行更新。

## <a name="connect-to-your-cluster-and-debug-a-service"></a>连接到群集并调试服务

在 Visual Studio 中打开 samples\todo-app\database-api\database-api.csproj。 在项目中，从启动设置下拉列表中选择“Bridge to Kubernetes”，如下所示。

![选择 Bridge to Kubernetes](media/bridge-to-kubernetes/choose-bridge-to-kubernetes.png)

单击 Bridge to Kubernetes 旁边的启动按钮。 在“为 Bridge to Kubernetes 创建配置文件”对话框中：

- 选择你的群集名称。
- 选择“todo-app”作为命名空间。
- 选择“database-api”作为要重定向到的服务。
- 选择之前用于启动浏览器的同一 URL： http://{external-ip}:{local-port}

![选择 Bridge to Kubernetes 群集](media/bridge-to-kubernetes/configure-bridge-debugging.png)

选择是否在隔离模式下运行，这意味着使用该群集的其他用户不会受到更改的影响。 通过将请求路由到每个受影响的服务的副本，但正常路由所有其他流量，可以实现此隔离模式。 有关如何执行此操作的更多说明，请参阅 [Bridge to Kubernetes 的工作原理][btk-overview-routing]。

单击 **“确定”** 。 将 Kubernetes 群集中 database-api 服务的所有流量重定向到开发计算机中运行的应用程序版本。 Bridge to Kubernetes 还会将应用程序的所有出站流量路由回 Kubernetes 群集。

> [!NOTE]
> 系统将提示你允许 EndpointManager 在提升的权限下运行并修改主机文件。

当状态栏显示你已连接到 `database-api` 服务时，你的开发计算机已连接。

![已连接开发计算机](media/bridge-to-kubernetes/development-computer-connected.png)

> [!NOTE]
> 在后续启动时，系统不会提示“创建 Bridge to Kubernetes 的配置文件”对话框。 可在项目属性的“调试”中更新这些设置。

连接开发计算机后，流量将开始重定向到你要替换的服务的开发计算机。

> [!NOTE]
> 例如，若要在之后编辑调试配置文件，则在希望使用不同的 Kubernetes 服务进行测试时，请选择“调试” > “调试属性”，然后单击“更改”按钮  。

## <a name="set-a-break-point"></a>设置断点

打开 MongoHelper.cs，并单击 CreateTask 方法中第 68 行处的某个位置，将光标置于该处。 若要设置断点，请按 F9，或选择“调试” > “切换断点” 。

通过打开公共 URL（前端服务的外部 IP 地址），导航到示例应用程序。 若要恢复服务，请按“F5”，或单击“调试” > “继续”  。

将光标置于断点所在的行上，然后按 F9，即可删除该断点。

> [!NOTE]
> 默认情况下，停止调试任务也会断开开发计算机与 Kubernetes 群集的连接。 你可以更改此行为，方法是在“工具” > “选项”对话框的“Kubernetes 调试工具”部分中将“调试后断开连接”更改为 `false`   。 更新此设置后，在停止并启动调试时，开发计算机将保持连接状态。 若要断开开发计算机与群集的连接，请单击工具栏上的“断开连接”按钮。
>
>![Kubernetes 调试选项的屏幕截图](media/bridge-to-kubernetes/kubernetes-debugging-options.png)

## <a name="additional-configuration"></a>其他配置

Bridge to Kubernetes 可以处理路由流量和复制环境变量，无需任何其他配置。 如果需要下载已装载到 Kubernetes 群集中的容器的所有文件（例如 ConfigMap 文件），可以创建 `KubernetesLocalProcessConfig.yaml` 以将这些文件下载到开发计算机。 有关详细信息，请参阅[将 KubernetesLocalProcessConfig.yaml 用于 Bridge to Kubernetes 的附加配置][kubernetesLocalProcessConfig-yaml]。

## <a name="using-logging-and-diagnostics"></a>使用日志记录和诊断

可在开发计算机的 TEMP 目录的 `Bridge to Kubernetes` 目录中查找诊断日志。

## <a name="next-steps"></a>后续步骤

了解 Bridge to Kubernetes 的工作原理。

> [!div class="nextstepaction"]
> [Bridge to Kubernetes 的工作原理](overview-bridge-to-kubernetes.md)

[todo-app-github]: https://github.com/Microsoft/mindaro
[supported-regions]: https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service
[troubleshooting]: /azure/dev-spaces/troubleshooting#fail-to-restore-original-configuration-of-deployment-on-cluster
[visual-studio]: https://www.visualstudio.com/vs/
[btk-extension]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.mindaro
[kubernetesLocalProcessConfig-yaml]: configure-bridge-to-kubernetes.md
[btk-overview-routing]: overview-bridge-to-kubernetes.md#using-routing-capabilities-for-developing-in-isolation
