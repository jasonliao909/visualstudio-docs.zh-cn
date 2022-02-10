---
title: 什么是Bridge to Kubernetes？
ms.technology: bridge
ms.custom: contperf-fy22q1
ms.date: 11/19/2020
ms.topic: overview
description: 介绍如何使用 Bridge to Kubernetes 将开发计算机连接到 Kubernetes 群集
keywords: Bridge to Kubernetes, Docker, Kubernetes, Azure, 容器
manager: jmartens
author: ghogen
ms.author: ghogen
ms.openlocfilehash: bcc09886dc6daae1e777cf0687913ff1420e527b
ms.sourcegitcommit: b9c5ca58f380ee102153b69656cb062b3d2dab8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/10/2022
ms.locfileid: "138427719"
---
# <a name="how-bridge-to-kubernetes-works"></a>Kubernetes 桥接的工作原理

*Bridge to Kubernetes* 是一种迭代开发工具，用于创作面向 Kubernetes 的微服务应用程序。 Bridge to Kubernetes扩展可用于Visual Studio Visual Studio Code (VS Code) 。

Bridge to Kubernetes允许在开发计算机上运行和调试代码。 该计算机仍使用应用程序或服务的其余部分连接到 Kubernetes 群集。 如果具有具有许多相互依赖的服务和数据库的大型微服务体系结构，则很难在开发计算机上复制这些依赖项。 每次代码更改时，生成代码并部署到 Kubernetes 群集可能会很慢、耗时且困难。

Bridge to Kubernetes在开发计算机和群集之间创建连接。 此方法可避免生成代码并部署到群集。 可以在连接到群集的上下文中测试和开发服务。 此方法允许你进行调试，而无需创建任何其他 Docker 或 Kubernetes 配置。

Bridge to Kubernetes 可重定向已连接的 Kubernetes 群集与开发计算机之间的流量。 Kubernetes 群集中的本地代码和服务可以像在同一 Kubernetes 群集中一样进行通信。

Bridge to Kubernetes将 Kubernetes 群集中的环境变量和装载的卷复制到开发计算机。 通过访问环境变量和已装载的卷，无需复制这些依赖项即可处理代码。

## <a name="requirements"></a>要求

若要Bridge to Kubernetes，需要以下配置之一：

- VS Code安装了 Bridge to Kubernetes [扩展。](https://aka.ms/bridge-to-k8s-vsc-extension)
- [Visual Studio 2019][visual-studio] 版本 16.7 或更高版本，Windows 10或更高版本。 请确保已安装 *ASP.NET 和 Web 开发* 工作负载。 安装 [Bridge to Kubernetes 扩展][btk-extension]。

可以使用 Bridge to Kubernetes 与 Kubernetes 群集建立连接。 此连接将群集中现有 Pod 的流量重定向到开发计算机。此连接将流量重定向到开发计算机。

> [!NOTE]
> 使用 Bridge to Kubernetes 时，系统将提示你输入要重定向到开发计算机的服务的名称。 使用此选项可以方便地识别用于重定向的 pod。 Kubernetes 群集与开发计算机之间的所有重定向都适用于 pod。 有关详细信息，请参阅 [使服务可用](configure-bridge-to-kubernetes.md#make-a-service-available)。

在 VS Code中，Bridge to Kubernetes支持所有语言，只要可以在本地运行它们。 在 Visual Studio 中，Bridge to Kubernetes支持 .NET Core。 Bridge to Kubernetes不支持在 .NET Framework 中Visual Studio，因为它需要Windows节点支持。

> [!CAUTION]
> Bridge to Kubernetes 仅适用于开发和测试场景。 它不适合用于生产群集或正在使用的实时服务，也不支持这样做。

有关当前功能和将来的计划，请参阅Bridge to Kubernetes [路线图](https://github.com/microsoft/mindaro/projects/1)。

## <a name="establishing-a-connection"></a>建立连接

当Bridge to Kubernetes与群集建立连接时，它会执行以下操作：

- 提示你在群集上配置要替换的服务，在开发计算机上配置用于代码的端口，并将代码的启动任务配置为一次性操作。
- 将群集上 pod 中的容器替换为远程代理容器，它会将流量重定向到开发计算机。
- 在开发计算机上运行 [kubectl port-forward][kubectl-port-forward]，将流量从开发计算机转发到群集中运行的远程代理。
- 使用远程代理从群集收集环境信息。 此环境信息包括环境变量、可见服务、卷装载和机密装载。
- 在 Visual Studio 中设置环境，以便开发计算机上的服务可以访问相同变量，就像它在该群集上运行一样。
- 更新 *主机文件* ，将群集上的服务映射到开发计算机上的本地 IP 地址。 *这些主机* 文件条目允许开发计算机上运行的代码向群集中运行的其他服务请求。 若要更新 *主机文件* ，Bridge to Kubernetes计算机上需要管理员访问权限。
- 开始在开发计算机上运行和调试代码。 如有必要，Bridge to Kubernetes停止当前使用这些端口的服务或进程，释放开发计算机上所需的端口。

## <a name="using-bridge-to-kubernetes"></a>使用 Bridge to Kubernetes

与群集建立连接后，在计算机上以本机方式运行和调试代码，而无需容器化。 代码与群集交互。 远程代理接收的任何网络流量都重定向到连接期间指定的本地端口。 本机运行的代码可以接受并处理该流量。 群集中的环境变量、卷和机密可供开发计算机上运行的代码使用。

Bridge to Kubernetes *主机文件* 条目和端口转发添加到开发人员计算机。 代码可以使用群集中的服务名称将网络流量发送到群集上运行的服务。 该流量将转发到群集中运行的服务。 在整个连接期间，流量在开发计算机和群集之间路由。

此外，Bridge to Kubernetes 还提供了一种方法，通过 `KubernetesLocalProcessConfig.yaml` 文件复制开发计算机中可用于群集中 Pod 的环境变量和已装载的文件。 还可以使用此文件创建新的环境变量和卷装载。

> [!NOTE]
> 在连接到群集期间加上 15 分钟，Bridge to Kubernetes在本地计算机上运行名为 *EndpointManager* 的进程。

可以使用多个服务并行调试。 启动多个实例Visual Studio要调试的服务一样。 确保服务在本地侦听不同的端口。 单独配置和调试它们。 此方案不支持隔离。

### <a name="additional-configuration"></a>其他配置

*KubernetesLocalProcessConfig.yaml* 文件允许复制可用于群集中 Pod 的环境变量和已装载文件。 使用 Visual Studio时，*KubernetesLocalConfig.yaml* 文件必须与服务的项目文件位于同一目录中。 有关详细信息，请参阅[配置 Bridge to Kubernetes][using-config-yaml]。

### <a name="using-routing-capabilities-for-developing-in-isolation"></a>使用路由功能进行独立开发

默认情况下，Bridge to Kubernetes 将单个服务的所有流量重定向到开发计算机。 可以改为使用路由功能仅将请求从子域重定向到开发计算机。 通过这些路由功能，你可以使用 Bridge to Kubernetes 在隔离模式下进行开发，从而避免中断群集中的其他流量。

以下动画显示了两个开发者独立处理同一群集：

![动画显示隔离，两个开发人员使用同一群集。](media/bridge-to-kubernetes/btk-graphic-isolated.gif)

启用隔离工作时，Bridge to Kubernetes除了连接到 Kubernetes 群集外，还执行以下操作：

- 验证 Kubernetes 群集是否未启用 Azure Dev Spaces。
- 复制同一命名空间的群集中的所选服务，并添加 routing.visualstudio.io/route-from=SERVICE_NAME 标签和 routing.visualstudio.io/route-on-header=kubernetes-route-as=GENERATED_NAME 注释。 
- 在 Kubernetes 群集上的同一命名空间中配置并启动路由管理器。 在命名空间中配置路由时，路由管理器 *routing.visualstudio.io/route-from=SERVICE_NAME 标签和* routing.visualstudio.io/route-on-header=kubernetes-route-as=GENERATED_NAME 批注。

> [!NOTE]
> Bridge to Kubernetes检查Azure Dev Spaces Kubernetes 群集上是否启用了此配置。 它会提示你先禁用Azure Dev Spaces，然后才能使用Bridge to Kubernetes。

路由管理器在启动时执行以下操作：

- 使用子域的 GENERATED_NAME 复制命名空间中发现的所有入口（ *包括负载均衡器* 入口）。
- 使用 GENERATED_NAME 子域为与复制的流入量关联的每个服务创建 envoy pod。
- 为正在独立处理的服务创建另一个 Envoy Pod。 此配置允许将子域的请求路由到开发计算机。
- 为每个 envoy pod 配置传递规则，以处理包含子域的服务的路由。

下图显示了在 Bridge to Kubernetes 连接到群集之前的 Kubernetes 群集：

![不带任何元素的Bridge to Kubernetes。](media/bridge-to-kubernetes/kubernetes-cluster.svg)

下图显示了在隔离模式下启用 Bridge to Kubernetes 的同一集群。 从该图中，你可以看到复制服务和支持独立路由的 envoy pod。

![已启用群集的Bridge to Kubernetes关系图。](media/bridge-to-kubernetes/kubernetes-cluster-dev-computer.svg)

当群集收到包含 GENERATED_NAME 域的请求时，它会将 *kubernetes-route-as=* GENERATED_NAME标头添加到该请求。 Envoy pod 负责将该请求路由到群集中的相应服务。 对于对独立处理的服务的请求，群集会将请求重定向到远程代理的开发计算机。

当群集收到请求而不GENERATED_NAME域时，它不会向请求添加标头。 Envoy pod 负责将该请求路由到群集中的相应服务。 对于正在替换的服务的请求，该 pod 会将其路由到原始服务而不是远程代理。

> [!IMPORTANT]
> 发出额外请求时，群集上的每个服务都必须转发 kubernetes-route-as=GENERATED_NAME 标头。 例如，当 serviceA 收到请求时，它会先向 serviceB 发出请求，然后再返回响应 。 在此示例中，serviceA 需要将其请求中的 kubernetes-route-as=GENERATED_NAME 标头转发到 serviceB  。 某些语言（如 [ASP.NET][asp-net-header]）可能具有处理标头传播的方法。

断开与群集的连接时，默认情况下，桥接到 Kubernetes 会删除所有 envoy pod 和重复的服务。

> [!NOTE]
> 路由管理器部署和服务在你的命名空间中保持运行。 要删除部署和服务，请对命名空间运行以下命令。
>
> ```azurecli
> kubectl delete deployment routingmanager-deployment -n NAMESPACE
> kubectl delete service routingmanager-service -n NAMESPACE
> ```

### <a name="diagnostics-and-logging"></a>诊断和日志记录

使用 Bridge Kubernetes 连接到群集时，计算机将记录诊断。 它将其存储在你的开发计算机的 *TEMP* 目录中，并将其存储在 *Kubernetes* 文件夹中。

### <a name="kubernetes-rbac-authorization"></a>Kubernetes RBAC 授权

Kubernetes 提供了基于角色的访问控制 (RBAC) 来管理用户和组的权限。 有关信息，请参阅 [Kubernetes 文档](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)。 可以通过创建 YAML 文件并使用 `kubectl` 将其应用于群集，来设置启用了 RBAC 的群集的权限。

若要设置群集的权限，请创建或修改 YAML 文件，例如 *docker-compose.override.yml*。 将命名空间用于 `<namespace>` 和需要访问的用户和组。

```yml
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: bridgetokubernetes-<namespace>
  namespace: development
subjects:
  - kind: User
    name: jane.w6wn8.k8s.ginger.eu-central-1.aws.gigantic.io
    apiGroup: rbac.authorization.k8s.io
  - kind: Group
    name: dev-admin
    apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: admin
  apiGroup: rbac.authorization.k8s.io
```

使用以下命令应用权限：

```cmd
kubectl -n <namespace> apply -f <yaml file name>
```

## <a name="limitations"></a>限制

Bridge to Kubernetes 具有以下限制：

- 要使 Bridge to Kubernetes 成功连接，一个 pod 只能有一个容器在该 pod 中运行。
- 目前，Bridge to Kubernetes pod 必须是 Linux 容器。 不支持 Windows 容器。
- Bridge to Kubernetes 需要提升的权限才能在开发计算机上运行，以便编辑主机文件。
- Bridge to Kubernetes 不能用于已启用 Azure Dev Spaces 的群集。

## <a name="next-steps"></a>后续步骤

若要开始使用 Bridge to Kubernetes 将本地开发计算机连接到群集，请参阅[使用 Bridge to Kubernetes (VS)](bridge-to-kubernetes-vs.md) 或[使用 Bridge to Kubernetes (VS Code)](bridge-to-kubernetes-vs-code.md)。

[asp-net-header]: https://www.nuget.org/packages/Microsoft.AspNetCore.HeaderPropagation/
[azds-cli]: /azure/dev-spaces/how-to/install-dev-spaces#install-the-client-side-tools
[azds-tmp-dir]: /azure/dev-spaces/troubleshooting#before-you-begin
[azure-cli]: /cli/azure/install-azure-cli?view=azure-cli-latest&preserve-view=true
[bridge-to-kubernetes-vs]: bridge-to-kubernetes.md
[kubectl-port-forward]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#port-forward
[visual-studio]: https://visualstudio.microsoft.com/downloads/
[btk-extension]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.mindaro
[using-config-yaml]: configure-bridge-to-kubernetes.md
