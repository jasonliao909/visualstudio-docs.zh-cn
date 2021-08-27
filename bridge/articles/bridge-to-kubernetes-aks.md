---
ms.topic: quickstart
ms.author: ghogen
author: ghogen
manager: jmartens
ms.technology: bridge
ms.custom: contperf-fy22q1
title: 在 Azure AKS 中使用 Bridge to Kubernetes 在本地运行和调试 Kubernetes
ms.date: 11/12/2020
description: 了解如何使用 Bridge to Kubernetes 将开发计算机连接到 AKS Kubernetes 群集
ms.openlocfilehash: ac2edf574426c7bef73ec68df38665500049de89
ms.sourcegitcommit: f930bc28bdb0ba01d6f7cb48f229afecfa0c90cd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2021
ms.locfileid: "122334597"
---
# <a name="use-bridge-to-kubernetes-with-aks"></a>在 AKS 中使用 Bridge to Kubernetes

在本教程中，你将使用特定的 AKS 示例微服务 Web 应用来了解如何使用 Bridge to Kubernetes 在属于 Azure Kubernetes 服务 (AKS) 群集的单个 Pod 中进行本地调试。

## <a name="before-you-begin"></a>在开始之前

本指南使用[自行车共享示例应用程序][bike-sharing-github]演示如何将开发计算机连接到在 AKS 中运行的 Kubernetes 群集。 如果你已在 Kubernetes 群集上运行自己的应用程序，请参阅[使用 Kubernetes 进行开发](bridge-to-kubernetes-vs-code.md)。 如果你使用的是另一个群集，例如在本地运行的 MiniKube，请参阅[通过示例来使用 Bridge to Kubernetes](bridge-to-kubernetes-sample.md)。

### <a name="prerequisites"></a>必备条件

* Azure 订阅。 如果没有 Azure 订阅，可以创建一个[免费帐户](https://azure.microsoft.com/free)。
* [已安装 Azure CLI][azure-cli]。
* 在 macOS、Windows 10 或 Linux 上运行的 [Visual Studio Code][vs-code]。
* 已在 Visual Studio Code 中安装 [Bridge to Kubernetes][btk-vs-code] 扩展。

## <a name="create-a-kubernetes-cluster"></a>创建 Kubernetes 群集

在[支持的区域][supported-regions]中创建 AKS 群集。 以下命令创建一个名为 `MyResourceGroup` 的资源组，以及一个名为 `MyAKS` 的 AKS 群集。

```azurecli-interactive
az group create \
    --name MyResourceGroup \
        --location eastus
az aks create \
    --resource-group MyResourceGroup \
    --name MyAKS \
    --location eastus \
    --node-count 3 \
    --generate-ssh-keys
```

## <a name="install-the-sample-application"></a>安装示例应用程序

使用提供的脚本在群集上安装示例应用程序。 可以在开发计算机上运行此脚本，或者使用 [Azure Cloud Shell][azure-cloud-shell]。 使用群集和资源组的名称。

> [!IMPORTANT]
> 必须拥有群集的“所有者”或“参与者”访问权限才能运行此脚本。

```azurecli-interactive
git clone https://github.com/Microsoft/mindaro
cd mindaro/
chmod +x ./bridge-quickstart.sh
./bridge-quickstart.sh -g MyResourceGroup -n MyAKS
```

通过打开其公共 URL（显示在安装脚本的输出中），导航到运行群集的示例应用程序。

```console
$ ./bridge-quickstart.sh -g MyResourceGroup -n MyAKS
Checking directory /home/<user>/mindaro for GIT repo Microsoft/Mindaro
Setting the Kube context
...
To try out the app, open the url:
bikeapp.bikesharingweb.EXTERNAL_IP.nip.io
```

在上面的示例中，公共 URL 为 `bikeapp.bikesharingweb.EXTERNAL_IP.nip.io`。

## <a name="connect-to-your-cluster-and-debug-a-service"></a>连接到群集并调试服务

在开发计算机上，下载并配置 Kubernetes CLI 以使用 [az aks get-credentials][az-aks-get-credentials] 连接到 Kubernetes 群集。

```azurecli
az aks get-credentials --resource-group MyResourceGroup --name MyAKS
```

在 Visual Studio Code 中，从[自行车共享示例应用程序][bike-sharing-github]打开 `mindaro/samples/BikeSharingApp/Bikes`。 打开 Azure Kubernetes 服务扩展，并在 MyAKS 群集中选择 bikeapp 命名空间。 右键单击“bikeapp”节点，然后选择“使用命名空间”。

![选择命名空间](media/bridge-to-kubernetes-vs-code/select-namespace.png)

打开终端窗口（“终端”>“新建终端”），在终端窗口的“bikes”文件夹中，使用 `npm install` 命令安装应用程序的依赖项。

```console
npm install
```

打开命令面板（CTRL+SHIFT+P 或 Cmd+Shift+P (Mac)），然后运行命令“Bridge to Kubernetes: 配置”以启动配置过程。

选择“bikes”服务。

![选择服务](media/bridge-to-kubernetes-vs-code/choose-service.png)

将 Kubernetes 群集中 bikes 服务的所有流量重定向到开发计算机中运行的应用程序版本。 Bridge to Kubernetes 还会将应用程序的所有出站流量路由回 Kubernetes 群集。

> [!IMPORTANT]
> 只能重定向仅有一个 pod 的服务。

选择服务后，系统会提示你输入本地应用程序的 TCP 端口。 在本例中，输入“3000”。

![连接所选端口](media/bridge-to-kubernetes-vs-code/choose-port.png)

选择“通过 NPM 启动”作为启动任务。

![连接所选启动任务](media/bridge-to-kubernetes-vs-code/choose-launch.png)

> [!NOTE]
> 系统将提示你允许 EndpointManager 在提升的权限下运行并修改主机文件。

可以选择在隔离或非隔离模式下运行。 如果在隔离模式下运行，则只有你的请求被路由到你的本地进程；其他开发人员可以使用群集而不受影响。 如果在非隔离模式下运行，则所有流量都被重定向到本地进程。 有关此选项的详细信息，请参阅[使用路由功能进行独立开发][btk-overview-routing]。

![隔离提示](media/bridge-to-kubernetes-vs-code/btk-isolation-prompt.png)

选择左侧的“调试”图标，然后选择顶部的“使用 Kubernetes 通过 NPM 启动”。

![选择 Bridge to Kubernetes](media/bridge-to-kubernetes-vs-code/choose-bridge-to-kubernetes.png)

当 VS Code 状态栏变为橙色且 Kubernetes 扩展显示已连接时，表示你的开发计算机已连接。

![已连接开发计算机](media/bridge-to-kubernetes-vs-code/development-computer-connected.png)

> [!NOTE]
> 在后续启动时，系统不会提示输入服务名称、端口、启动任务或者是否在隔离模式下运行。 这些值都保存在 `.vscode/tasks.json` 中。 若要稍后更改这些设置，请打开命令面板（CTRL+SHIFT+P 或 Cmd+Shift+P (Mac)），然后运行命令“Bridge to Kubernetes: 配置”。

连接开发计算机后，流量将开始重定向到你要替换的服务的开发计算机。

## <a name="set-a-break-point"></a>设置断点

打开 [server.js][server-js-breakpoint]，将光标置于第 233 行的某个位置。 使用 F9 设置断点，或选择“运行”，然后选择“切换断点”。

通过打开公共 URL 导航到示例应用程序。 选择“Aurelia Briggs (客户)”作为用户，然后选择要租赁的自行车。 请注意，自行车的图像没有加载。 返回 Visual Studio Code，会看到第 233 行已突出显示。 你设置的断点已在第 233 行暂停了服务。 若要恢复服务，请按 F5 或选择“运行”，然后选择“继续”。 返回浏览器，验证是否看到自行车的占位符图像。

通过将光标置于 `server.js` 中的第 233 行并按 F9 来删除断点。

### <a name="update-your-application"></a>更新应用程序

编辑 `server.js` 以删除第 234 行和 235 行：

```javascript
    // Hard code image url *FIX ME*
    theBike.imageUrl = "/static/logo.svg";
```

该节现在应如下所示：

```javascript
    var theBike = result;
    theBike.id = theBike._id;
    delete theBike._id;
```

保存更改，然后按 Ctrl+Shift+F5（在 Mac 上，按 ⇧⌘F5），或选择“运行”，然后选择“重新启动调试”。 重新连接后，刷新浏览器并验证是否不再看到自行车的占位符图像。

选择“运行”，然后选择“停止调试”，或按 Shift+F5 以停止调试器。

> [!NOTE]
> 默认情况下，停止调试任务也会断开开发计算机与 Kubernetes 群集的连接。 可以通过以下方法更改此行为：在 Visual Studio Code 设置中搜索“Bridge to Kubernetes: 调试后断开连接”，并取消选中“调试结束后自动断开连接”旁边的复选框。 更新此设置后，在停止并启动调试时，开发计算机将保持连接状态。 若要断开开发计算机与群集的连接，请单击状态栏上的 Bridge to Kubernetes 扩展，然后选择“断开当前会话连接”。

## <a name="additional-configuration"></a>其他配置

Bridge to Kubernetes 可以处理路由流量和复制环境变量，无需任何其他配置。 如果需要从其他命名空间本地复制服务，或下载已装载到 Kubernetes 群集中的容器的所有文件（例如 ConfigMap 文件），可以创建 `KubernetesLocalProcessConfig.yaml` 以将这些文件下载到开发计算机。 有关详细信息，请参阅[配置 Bridge to Kubernetes][kubernetesLocalProcessConfig-yaml]。

## <a name="using-logging-and-diagnostics"></a>使用日志记录和诊断

在开发计算机连接到 Kubernetes 群集后，日志记录输出将写入“Bridge to Kubernetes”窗口。

![日志记录输出](media/bridge-to-kubernetes-vs-code/output.png)

单击“Kubernetes”状态栏，然后选择“显示连接诊断信息”。 此命令在日志记录输出中打印当前环境变量和 DNS 条目。

![包含诊断的输出](media/bridge-to-kubernetes-vs-code/output-diagnostics.png)

此外，还可以在开发计算机的 TEMP 目录的 `Bridge to Kubernetes` 目录中查找诊断日志。 在 Windows 10 上，位于 `%TEMP%\Bridge to Kubernetes` 中。 在 Mac 上，可以通过从终端窗口运行 `echo $TMPDIR` 找到 TEMP 目录。 在 Linux 上，位于 `/tmp/Bridge to Kubernetes` 中。

## <a name="running-in-isolation-mode"></a>在隔离模式下运行

使用 Bridge to Kubernetes，还可以设置正在处理的服务的隔离版本，这意味着使用该群集的其他人不会受到更改的影响。 通过将请求路由到每个受影响的服务的副本，但正常路由所有其他流量，可以实现此隔离模式。 有关如何执行此操作的更多说明，请参阅 [Bridge to Kubernetes 的工作原理][btk-overview-routing]。

## <a name="remove-the-sample-application-from-your-cluster"></a>从群集中删除示例应用程序

使用提供的脚本从群集中删除示例应用程序。

```azurecli-interactive
./bridge-quickstart.sh -c -g MyResourceGroup -n MyAKS
```

## <a name="troubleshooting"></a>故障排除

 如果在激活 Bridge to Kubernetes 扩展时出现以下错误：

“无法更新依赖项: 超出最大重试次数”

 首先，使用按钮重试激活。 如果反复失败，请参阅 [https://github.com/microsoft/mindaro/issues/32](https://github.com/microsoft/mindaro/issues/32)。

## <a name="next-steps"></a>后续步骤

若要详细了解 Bridge to Kubernetes，请参阅 [Bridge to Kubernetes 工作原理][btk-how-it-works]。

[azure-kubernetes-service]: /azure/aks/kubernetes-walkthrough
[azds-cli]: /azure/dev-spaces/how-to/install-dev-spaces#install-the-client-side-tools
[azds-tmp-dir]: /azure/dev-spaces/troubleshooting#before-you-begin
[btk-vs-code]: https://marketplace.visualstudio.com/items?itemName=mindaro.mindaro
[azure-cli]: /cli/azure/install-azure-cli?view=azure-cli-latest&preserve-view=true
[azure-cloud-shell]: /azure/cloud-shell/overview
[az-aks-get-credentials]: /cli/azure/aks?view=azure-cli-latest&preserve-view=true#az-aks-get-credentials
[az-aks-vs-code]: https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-aks-tools
[bike-sharing-github]: https://github.com/Microsoft/mindaro
[preview-terms]: https://azure.microsoft.com/support/legal/preview-supplemental-terms/
[server-js-breakpoint]: https://github.com/Microsoft/mindaro/blob/master/samples/BikeSharingApp/Bikes/server.js#L233
[supported-regions]: https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service
[troubleshooting]: /azure/dev-spaces/troubleshooting#fail-to-restore-original-configuration-of-deployment-on-cluster
[vs-code]: https://code.visualstudio.com/download
[kubernetesLocalProcessConfig-yaml]: configure-bridge-to-kubernetes.md
[btk-how-it-works]: overview-bridge-to-kubernetes.md
[btk-overview-routing]: overview-bridge-to-kubernetes.md#using-routing-capabilities-for-developing-in-isolation
