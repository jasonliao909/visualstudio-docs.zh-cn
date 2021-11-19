---
title: 通过 Bridge 同时调试多个服务与 Kubernetes
ms.date: 6/2/2021
description: 了解如何使用 Bridge Kubernetes 将开发计算机连接到 Kubernetes 群集，并使用本地隧道调试同时调试多个服务，Visual Studio Code。
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: bridge
ms.custom: contperf-fy22q1
ms.topic: how-to
ms.openlocfilehash: 195f0d29bad8f653ef99d9e2359d3250c6694536
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832950"
---
# <a name="debug-multiple-services-vs-code"></a>调试多个服务 (VS Code) 

桥接 Kubernetes 提供了在本地环境中调试 Kubernetes 服务的功能，如[使用 Bridge 到 Kubernetes (VS Code) ](bridge-to-kubernetes-vs-code.md)中所述。 使用 Bridge 到 Kubernetes，可以将流量重定向到服务的本地运行实例，并可使用 VS Code 的调试器进行调试。 但是，在某些情况下，你想要使用多个服务并同时调试它们。 通过执行以下步骤，可以并行调试多个服务。

## <a name="to-debug-multiple-services-at-the-same-time"></a>同时调试多个服务

1. 请确保服务在本地侦听不同端口。 端口号是特定于服务的，因此请查看服务代码以确定其侦听的端口。 如果要调试的多个服务在相同端口上进行侦听，将无法同时调试它们。

1. 打开与 VS Code 中的第一个服务对应的文件夹。

1. 在 VS Code 中，选择 "**文件**" "  >  **将文件夹添加到工作区 ...**"，并选择对应于其他服务的文件夹。

1. 在 Mac) 上打开 "命令" 面板 (" **CTRL** + **shift** + **p** " 或 " **Cmd** + **shift** + **p** "，然后对每个服务运行命令 **网桥**，并完成配置步骤。

    > [!WARNING]
    > 如果将服务配置为单独运行，请确保它们在文件中使用相同的 **isolateAs** 值 `.vscode/tasks.json` 。 此值是桥接于 Kubernetes 用于将隔离服务的流量定向到的前缀。 默认情况下，配置这些值时，它们具有不同的值。 您可以选择其中一个值，并为 `tasks.json` 其他服务手动编辑文件，以便为它们指定相同的值。
    >
    > ```json
    > "tasks": [
    >    {
    >        "label": "bridge-to-kubernetes.service",
    >        "type": "bridge-to-kubernetes.service",
    >        "service": "service-name",
    >        "ports": [
    >            3000
    >        ],
    >        "isolateAs": "<copy-same-value-for-all-debugged-services>",
    >        "useKubernetesServiceEnvironmentVariables": false
    >    }
    >]
    > ```

1. 在每个服务中设置所需的任何断点。

1. 对于每个服务，通过在每个服务文件夹中启动调试器，开始调试 (按 **F5**) 。 上一步为每个服务创建了启动配置，在从该工作区启动 VS Code 调试器时，VS Code 的调试器使用此配置。

## <a name="next-steps"></a>后续步骤

详细了解 bridge 到 Kubernetes[的工作原理。](overview-bridge-to-kubernetes.md)
