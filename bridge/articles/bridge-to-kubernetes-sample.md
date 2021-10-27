---
ms.topic: quickstart
ms.author: ghogen
author: ghogen
manager: jmartens
ms.technology: bridge
ms.custom: contperf-fy22q1
title: 了解如何借助 TODO 示例应用使用 Bridge to Kubernetes 在本地运行和调试 Kubernetes。
ms.date: 10/20/2020
description: 借助 TODO 示例应用，了解如何使用 Bridge to Kubernetes 在 Visual Studio Code 中本地开发、调试和测试 Kubernetes 应用程序
ms.openlocfilehash: 483819e102d0eca1048763ff5d28a3143accb98e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126652396"
---
# <a name="use-bridge-to-kubernetes-with-a-sample"></a>通过示例来使用 Bridge to Kubernetes

此示例演示如何使用 Bridge to Kubernetes 在任何 Kubernetes 群集上开发简单的 TODO 应用程序的微服务版本。 这个使用 Visual Studio Code 的示例由 [TodoMVC](https://todomvc.com) 提供的代码改编而来。 在本示例中，我们使用 MiniKube 来托管应用程序，但这些步骤适用于任何 Kubernetes 群集。

TODO 应用程序示例由提供持久存储的前端和后端组成。 此扩展示例添加了一个统计信息组件，并将应用程序分解为多个微服务，具体如下：

- 前端调用 database-api 来保留和更新 TODO 项；
- database-api 服务依赖于 Mongo 数据库来保留 TODO 项；
- 前端将添加、完成和删除事件写入 RabbitMQ 队列；
- 统计信息工作者从 RabbitMQ 队列接收事件，并更新 Redis 缓存；
- 统计信息 API 公开缓存的统计数据供前端显示。

总之，此扩展 TODO 应用程序由六个相关组件组成。

## <a name="prerequisites"></a>先决条件

- 任何 Kubernetes 群集，或 [Chocolatey](https://chocolatey.org/) 包管理器，用于安装 MiniKube
- 在 Windows 10 上已有 [Hyper-V](/virtualization/hyper-v-on-windows)
- 已安装 [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)，且安装在所选命令行环境中的路径上
- [Bridge to Kubernetes](https://aka.ms/bridge-to-k8s-vsc-extension) Visual Studio Code 扩展

## <a name="install-minikube"></a>安装 MiniKube

可以将任何 Kubernetes 提供程序与 Bridge to Kubernetes 一起使用。 在本文中，我们使用 MiniKube。 MiniKube 是一种轻量级 Kubernetes 提供程序，可让你在本地计算机上托管 Kubernetes。 请按照[安装说明](https://minikube.sigs.k8s.io/docs/start/)在 Windows 10、Linux 或 macOS 上安装 MiniKube。

为了在 Windows 10 上获得最佳结果，应使用 Hyper-V VM 管理器并创建一个[虚拟交换机](/windows-server/virtualization/hyper-v/get-started/create-a-virtual-switch-for-hyper-v-virtual-machines)。

安装后，启动 MiniKube，指定使用 Hyper-V，并提供主虚拟交换机的名称。 下面的命令必须使用管理员权限从命令提示符中运行。

```cmd
minikube start --vm-driver hyperv --hyperv-virtual-switch "Primary Virtual Switch"
```

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

如果要使用 MiniKube 进行测试，则需要使用 `minikube tunnel` 解析外部 IP。

```output
kubectl get services -n todo-app

NAME          TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)        AGE
frontend      LoadBalancer   10.0.49.177    127.0.0.1   80:30145/TCP   18h
```

使用外部 IP 和本地端口（“端口”列中的第一个数字）浏览到应用程序。

```input
http://{external-ip}:{local-port}
```

在浏览器中测试正在运行的应用。 在添加、完成和删除 todo 项时，请注意，统计信息页将以预期的指标进行更新。

## <a name="debug-the-stats-api-service"></a>调试 stats-api 服务

现在可以使用 Bridge to Kubernetes 扩展来演示如何将来自 Kubernetes 群集的流量重定向到本地运行的 stats-api 版本。

```cmd
cd stats-api/
```

在 VS Code 中打开 stats-api 的源代码。

```cmd
code .
```

启动 VS Code 后，从 VS Code 的左边栏中打开“Kubernetes”窗格，然后在 MiniKube 群集中选择“todo-app”命名空间。 右键单击“todo-app”节点，然后选择“使用命名空间”。

![选择命名空间](media/bridge-to-kubernetes-sample/select-namespace.png)

通过在终端窗口 (CTRL + ~) 中运行 `npm install` 来安装依赖项。

```cmd
npm install
```

接下来，在 `server.js` 的第 17 行上放置一个断点。

打开命令面板（CTRL+SHIFT+P 或 Cmd+Shift+P (Mac)），并键入 Bridge to Kubernetes。 选择“Bridge to Kubernetes: 配置”选项。

![“Bridge to Kubernetes: 配置”命令](media/bridge-to-kubernetes-sample/bridge-configure.png)

系统将提示你配置要替换的服务、要从开发计算机转发的端口，以及要使用的启动任务。

选择 `stats-api` 服务。

![选择要连接到的服务](media/bridge-to-kubernetes-sample/select-service.png)

选择服务后，系统会提示你输入本地应用程序的 TCP 端口。 在本例中，输入 3001。

![输入端口号](media/bridge-to-kubernetes-sample/enter-port.png)

选择“运行脚本: 开发”作为启动任务。

![选择调试器启动任务](media/bridge-to-kubernetes-sample/launch-task.png)

可以选择在隔离或非隔离模式下运行。 如果在隔离模式下运行，则只有你的请求被路由到你的本地进程；其他开发人员可以使用群集而不受影响。 如果在非隔离模式下运行，则所有流量都被重定向到本地进程。 有关此选项的详细信息，请参阅[使用路由功能进行独立开发](overview-bridge-to-kubernetes.md#using-routing-capabilities-for-developing-in-isolation)。 在本例中，我们将继续使用非隔离模式。

![选择隔离](media/bridge-to-kubernetes-sample/isolation.png)

> [!NOTE]
> 系统将提示你允许 EndpointManager 在提升的权限下运行并修改主机文件。

Bridge to Kubernetes 调试配置文件就已经配置成功了。

选择左侧的“调试”图标，然后选择“运行脚本: 使用 Kubernetes 开发”。 单击“运行脚本: 使用 Kubernetes 开发”旁边的“开始”按钮。

![选择调试启动配置文件](media/bridge-to-kubernetes-sample/debug-profile.png)

当 VS Code 状态栏变为橙色且 Kubernetes 扩展显示已连接时，表示你的开发计算机已连接。 连接开发计算机后，流量将开始重定向到你要替换的 stats-api 的开发计算机。

![使用 Bridge to Kubernetes 进行调试](media/bridge-to-kubernetes-sample/debugging.png)

导航到 todo-app 的前端入口点。 对于 minikube，我们将使用 `127.0.0.1`。 若要访问应用的本地终结点 URL，请打开状态栏上的“Kubernetes”菜单，然后选择终结点条目。

通过选择“统计信息”链接向 stats-api 发出请求。

![正在运行的网站 - 选择统计信息链接](media/bridge-to-kubernetes-sample/stats.png)

请注意，最初在群集中启动的流量已重定向到在其中触发了断点的本地运行的版本（在群集外）。

按下“播放”，让请求以透明的方式继续完成。

这个示例只展示了如何在非 AKS 群集上使用 Bridge to Kubernetes。  接下来在你自己的项目中试试吧！

## <a name="clean-up"></a>清理

若要清理此示例生成的资产，请运行：

```cmd
kubectl delete namespace todo-app
```

## <a name="next-steps"></a>后续步骤

你还可以使用 Bridge to Kubernetes 将应用部署到 Azure Kubernetes Service (AKS)。 请参阅[在 AKS 上使用 Bridge to Kubernetes](bridge-to-kubernetes-aks.md)
