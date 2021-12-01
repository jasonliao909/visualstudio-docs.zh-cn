---
ms.topic: quickstart
ms.author: ghogen
author: ghogen
manager: jmartens
ms.technology: bridge
ms.custom: contperf-fy22q1
title: 使用 Bridge to Kubernetes 在本地运行和调试 Kubernetes (VS Code)
ms.date: 04/14/2021
description: 了解如何使用 Bridge to Kubernetes将开发计算机连接到 Kubernetes 群集，并使用本地隧道调试在本地计算机上调试 Kubernetes 服务。
ms.openlocfilehash: 4e6117dc3b449f964feea367ab6de920f2e88259
ms.sourcegitcommit: d63ba1eff845d41ca095efb14b499ea96c4b6eba
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2021
ms.locfileid: "129561010"
---
# <a name="use-bridge-to-kubernetes-vs-code"></a>使用 Bridge to Kubernetes (VS Code)

通过 Bridge to Kubernetes，你可在开发计算机上运行和调试代码，而不中断 Kubernetes 群集与其余应用程序或服务的连接。 本指南介绍如何使用 Bridge to Kubernetes 来重定向 Kubernetes 群集与开发计算机上运行的代码之间的流量。

## <a name="before-you-begin"></a>在开始之前

本文假设你的群集具有微服务体系结构，并且你需要调试群集中的一个 Pod。 若要了解如何对现有示例应用程序使用 Bridge to Kubernetes，请参阅[通过示例来使用 Bridge to Kubernetes](bridge-to-kubernetes-sample.md)。 如果你使用的是 Azure Kubernetes 服务，并且需要使用一个更复杂的示例应用程序，请参阅 [Bridge to Kubernetes (AKS)](bridge-to-kubernetes-aks.md)。

### <a name="prerequisites"></a>必备条件

* 一个包含要调试的应用的 Kubernetes 群集。
* 在 macOS、Windows 10 或更高版本或 Linux 上运行的 [Visual Studio Code][vs-code]。

## <a name="connect-to-your-cluster-and-debug-a-service"></a>连接到群集并调试服务

有几种不同的方法可以启动使用 Bridge to Kubernetes 进行调试的过程。 如果你是从开放源代码的 Kubernetes 扩展开始使用，但没有安装Bridge to Kubernetes，请转到[安装并使用本地隧道调试](#install-and-use-local-tunnel-debugging)。 如果已安装 Bridge to Kubernetes，请继续执行以下步骤：

1. 在开发计算机上，确保当前上下文已设置为运行应用程序的群集和命名空间。

1. 打开要在 Visual Studio Code 中调试的应用的工作区。 在“群集”下的 Kubernetes 扩展视图中，确保已选择群集和命名空间。 打开命令面板（CTRL+SHIFT+P 或 Cmd+Shift+P (Mac)），然后运行命令“Bridge to Kubernetes: 配置”以启动配置过程。

1. 选择要重定向到本地版本的 Kubernetes 服务。

   ![选择要连接到的服务](media/bridge-to-kubernetes-sample/select-service.png)

   Kubernetes 群集中服务的所有流量都会重定向到开发计算机中运行的应用程序版本。 Bridge to Kubernetes 还会将应用程序的所有出站流量路由回 Kubernetes 群集。

   > [!IMPORTANT]
   > 只能重定向仅有一个 pod 的服务。

1. 选择服务后，跳过下一部分，然后按照[使用 Bridge to Kubernetes 配置调试器以进行本地隧道调试](#configure-the-debugger-for-local-tunnel-debugging-with-bridge-to-kubernetes)中的步骤继续操作。

## <a name="install-and-use-local-tunnel-debugging"></a>安装和使用本地隧道调试

安装了开放源代码的 [Kubernetes 扩展](https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools)，并拥有包含要调试的服务的 Kubernetes 群集后，按照以下步骤操作，开始使用本地隧道调试。 本节中的步骤将逐步安装 Bridge to Kubernetes 并启动本地隧道调试的配置过程。

> [!NOTE]
> 适用于 VS Code 的 Kubernetes 扩展提供了一个 API 入口点，使扩展创作者可以从 VS Code 市场提供其他本地隧道解决方案。 Bridge to Kubernetes 是本地隧道调试功能的一个可能的实现。

有两种方法可以开始在 VS Code 中使用本地隧道调试。 第一种方法是打开命令面板（CTRL+SHIFT+P 或 Cmd+Shift+P (Mac)），并键入“Kubernetes: 调试(本地隧道)”。

![显示 VS Code 中的“调试(本地隧道)”命令的屏幕截图](media/bridge-to-kubernetes-vs-code/debug-local-tunnel.png)

或者，导航到 Kubernetes 群集资源管理器。 打开活动群集的资源，并找到要调试的服务或 Pod，然后右键单击该服务并选择“调试: 本地隧道”。

此时，如果你还没有安装可提供本地调试功能的任何 VS Code 扩展，系统会将你重定向到市场以选择可提供本地调试的扩展。 选择“Bridge to Kubernetes”扩展。

![显示 VS Code 中的“调试本地隧道”快捷菜单的屏幕截图](media/bridge-to-kubernetes-vs-code/debug-local-tunnel-context-menu.png)

安装 Bridge to Kubernetes 扩展后，当你下次选择“调试: 本地隧道”时，将跳过安装步骤并直接继续执行下一步，即[使用 Bridge to Kubernetes 配置调试器以进行本地隧道调试](#configure-the-debugger-for-local-tunnel-debugging-with-bridge-to-kubernetes)。

## <a name="configure-the-debugger-for-local-tunnel-debugging-with-bridge-to-kubernetes"></a>使用 Bridge to Kubernetes 配置调试器以进行本地隧道调试

配置调试器以进行本地隧道调试的第一步是，系统会提示输入应用程序用于本地运行的 TCP 端口：

![输入端口号](media/bridge-to-kubernetes-sample/enter-port.png)

选择你在本地运行应用程序时通常使用的调试启动配置。 如果没有启动配置，可以让 Bridge to Kubernetes 创建一个启动配置，也可以选择不创建启动配置，在这种情况下必须手动启动应用程序或服务。 有关详细信息，请参阅[启动配置](https://code.visualstudio.com/docs/editor/debugging#_launch-configurations)。

![选择调试器启动配置](media/bridge-to-kubernetes-vs-code/choose-launch.png)

可以选择在隔离或非隔离模式下运行。 如果在隔离模式下运行，则只有你的请求被路由到你的本地进程；其他开发人员可以使用群集而不受影响。 如果在非隔离模式下运行，则所有流量都被重定向到本地进程。 有关此选项的详细信息，请参阅[使用路由功能进行独立开发][btk-overview-routing]。

![选择隔离](media/bridge-to-kubernetes-sample/isolation.png)

选择左侧的“调试”图标，然后在顶部选择新添加的 Kubernetes 启动配置，例如“使用 Kubernetes 通过 NPM 启动”。 如果选择该选项，将由 Bridge to Kubernetes 创建此启动配置。

![选择调试启动配置文件](media/bridge-to-kubernetes-sample/debug-profile.png)

> [!NOTE]
> 系统将提示你允许 EndpointManager 在提升的权限下运行并修改主机文件。

当 VS Code 状态栏变为橙色且 Kubernetes 扩展显示已连接时，表示你的开发计算机已连接。

![使用 Bridge to Kubernetes 进行调试](media/bridge-to-kubernetes-sample/debugging.png)

连接开发计算机后，流量将开始重定向到你要替换的服务的开发计算机。

> [!NOTE]
> 在后续启动时，系统不会提示输入服务名称、端口、启动任务或者是否在隔离模式下运行。 这些值都保存在 `.vscode/tasks.json` 中。 若要稍后更改这些设置，请打开命令面板（CTRL+SHIFT+P 或 Cmd+Shift+P (Mac)），然后运行命令“Bridge to Kubernetes: 配置”。 可以打开 .vscode/launch.json 和 .vscode/tasks.json 来查看 Bridge to Kubernetes 添加到启动配置文件的具体配置设置。
>
>如果你的群集使用 [gRPC C 核心](https://github.com/grpc/grpc/)（使用 [c-ares](https://github.com/c-ares/c-ares)的 gRPC 实现），则环境变量将添加到启动配置文件 GRPC_DNS_RESOLVER 中，且值为 `native`。 此变量指定使用一种解决方法，以避免在连接时出现 2 分钟的延迟。 有关详细信息，请参阅此 [gRPC 问题](https://github.com/grpc/grpc/issues/18691)。

## <a name="set-a-break-point"></a>设置断点

使用 F9 设置断点，或选择“运行”，然后选择“切换断点”。

通过打开公共 URL 导航到示例应用程序。 当代码到达断点时，它应会在调试器中打开。 若要恢复服务，请按 Ctrl+F5 或选择“运行”，然后选择“继续”。 返回浏览器，验证是否看到自行车的占位符图像。

### <a name="update-your-application"></a>更新应用程序

在本地进行代码更改时，它们是否对使用群集的其他人可见，取决于你是否在隔离模式下运行。 如果在隔离模式下运行，在做出更改后不会影响其他用户。

编辑代码，保存更改，然后按 Ctrl+Shift+F5（在 Mac 上，按 ⇧⌘F5），或选择“运行”，然后选择“重新启动调试”。 重新连接后，刷新浏览器并验证更改。

选择“运行”，然后选择“停止调试”，或按 Shift+F5 以停止调试器。

> [!NOTE]
> 默认情况下，停止调试任务也会断开开发计算机与 Kubernetes 群集的连接。 可以通过以下方法更改此行为：在 Visual Studio Code 设置中搜索“Bridge to Kubernetes: 调试后断开连接”，并取消选中“调试停止后自动断开连接”旁边的复选框。 更新此设置后，在停止并启动调试时，开发计算机将保持连接状态。 若要断开开发计算机与群集的连接，请单击状态栏上的 Bridge to Kubernetes 扩展，然后选择“断开当前会话连接”。

## <a name="additional-configuration"></a>其他配置

Bridge to Kubernetes 可以处理路由流量和复制环境变量，无需任何其他配置。 如果需要下载已装载到 Kubernetes 群集中的容器的所有文件（例如 ConfigMap 文件），可以创建 `KubernetesLocalProcessConfig.yaml` 以将这些文件下载到开发计算机。 有关详细信息，请参阅[配置 Bridge to Kubernetes][kubernetesLocalProcessConfig-yaml]。

如果你所用的是使用托管标识（Azure Active Directory 提供的一个安全功能）的 AKS 群集，请参阅[结合使用托管标识与 Bridge to Kubernetes](managed-identity.md)，了解如何为这种场景配置 Bridge to Kubernetes。

## <a name="using-logging-and-diagnostics"></a>使用日志记录和诊断

在开发计算机连接到 Kubernetes 群集后，日志记录输出将写入“Bridge to Kubernetes”窗口。

单击“Kubernetes”状态栏，然后选择“显示连接诊断信息”。 此命令在日志记录输出中打印当前环境变量和 DNS 条目。

此外，还可以在开发计算机的 TEMP 目录的 `Bridge to Kubernetes` 目录中查找诊断日志。 在 Windows 10 上，位于 `%TEMP%\Bridge to Kubernetes` 中。 在 Mac 上，可以通过从终端窗口运行 `echo $TMPDIR` 找到 TEMP 目录。 在 Linux 上，位于 `/tmp/Bridge to Kubernetes` 中。

## <a name="running-in-isolation-mode"></a>在隔离模式下运行

使用 Bridge to Kubernetes，还可以设置正在处理的服务的隔离版本，这意味着使用该群集的其他人不会受到更改的影响。 通过将请求路由到每个受影响的服务的副本，但正常路由所有其他流量，可以实现此隔离模式。 若要访问独立应用的本地终结点 URL，请以隔离模式启动调试器，打开状态栏上的 Kubernetes 菜单，然后选择终结点条目。 有关路由在隔离模式下的工作原理的更多信息，请参阅 [Bridge to Kubernetes 工作原理][btk-overview-routing]。

## <a name="header-propagation"></a>标头传播

若要按预期方式使用 Bridge to Kubernetes，需要确保将 Bridge to Kubernetes 标头从传入请求传播到服务向群集中的其他服务发出的任何请求。 所有 HTTP 请求 API（无论使用何种语言）都提供了一些特定于框架的方式来执行此操作。 例如，对于采用 C# 的 .NET 代码，你可以使用类似于下面的代码：

```csharp
var request = new HttpRequestMessage();
request.RequestUri = new Uri("http://mywebapi/api/values/1");
if (this.Request.Headers.ContainsKey("kubernetes-route-as"))
{
    // Propagate the dev space routing header
    request.Headers.Add("kubernetes-route-as", this.Request.Headers["kubernetes-route-as"] as IEnumerable<string>);
}
var response = await client.SendAsync(request);
```

> [!NOTE]
> 为了避免影响每个请求的代码，可以创建从 [System.Net.Http.DelegatingHandler](/dotnet/api/system.net.http.delegatinghandler) 继承的类，然后使用类似于前面的示例的代码重写 `SendAsync` 方法。 可以在 Web 上查找使用此技术的代码；例如，[在 Bridge to Kubernetes 中正确传播“kubernetes-route-as”](https://blogs.u2u.be/lander/post/2020/11/25/properly-propagating-kubernetes-route-as-in-bridge-to-kubernetes)。

对于 Node.js 服务，可以使用与以下内容类似的代码，该代码取自 [mindaro 存储库](https://github.com/Microsoft/mindaro)中的 todo-app 示例：

```js
    server.get("/api/stats", function (req, res) {
        var options = {
            host: process.env.STATS_API_HOST,
            path: '/stats',
            method: 'GET'
        };
        const val = req.get('kubernetes-route-as');
        if (val) {
            console.log('Forwarding kubernetes-route-as header value - %s', val);
            options.headers = {
                'kubernetes-route-as': val
            }
        }
        var req = http.request(options, function(statResponse) {
            res.setHeader('Content-Type', 'application/json');
            var responseString = '';
            //another chunk of data has been received, so append it to `responseString`
            statResponse.on('data', function (chunk) {
                responseString += chunk;
            });
            statResponse.on('end', function () {
                res.send(responseString);
            });
        });

        req.on('error', function(e) {
            console.log('problem with request: ' + e.message);
          });

          req.end();
    });
```

## <a name="communicating-with-other-services"></a>与其他服务通信

与同一 Kubernetes 群集中的另一个服务（例如与 HTTP 请求）通信时，通常会在请求的 URL 中使用硬编码的服务名称，但在某些情况下是行不通的，例如，在使用远程 SSH、WSL 和 Codespaces 时。 [本文](kubernetes-environment-variables.md)介绍了如何使用 Kubernetes 服务环境变量指定这些场景的连接 URL。

## <a name="troubleshooting"></a>故障排除

 如果在激活 Bridge to Kubernetes 扩展时出现以下错误：

“无法更新依赖项: 超出最大重试次数”

 首先，使用按钮重试激活。 如果反复失败，请参阅 [https://github.com/microsoft/mindaro/issues/32](https://github.com/microsoft/mindaro/issues/32)。

在远程 SSH 会话中使用 Bridge to Kubernetes 时，如果 EndpointManager 失败，则问题可能是 Bridge to Kubernetes 由于权限问题而无法修改主机文件。 若要启用远程 SSH 或以非提升用户的身份运行，应更新代码以使用 Kubernetes 服务环境变量，并配置 VS Code 以使用它们，如[服务环境变量](kubernetes-environment-variables.md)主题中所述。

## <a name="next-steps"></a>后续步骤

若要详细了解 Bridge to Kubernetes，请参阅 [Bridge to Kubernetes 工作原理][btk-how-it-works]。

如果需要同时并行调试多个服务，请参阅[同时调试多个服务](parallel-services.md)。

有关当前支持的功能以及 Bridge to Kubernetes 的未来路线图，请访问 [Bridge to Kubernetes 路线图](https://github.com/microsoft/mindaro/projects/1)。

[azure-kubernetes-service]: /azure/aks/kubernetes-walkthrough
[azds-cli]: /azure/dev-spaces/how-to/install-dev-spaces#install-the-client-side-tools
[azds-tmp-dir]: /azure/dev-spaces/troubleshooting#before-you-begin
[btk-vs-code]: https://marketplace.visualstudio.com/items?itemName=mindaro.mindaro
[azure-cli]: /cli/azure/install-azure-cli
[azure-cloud-shell]: /azure/cloud-shell/overview
[az-aks-get-credentials]: /cli/azure/aks#az-aks-get-credentials
[az-aks-vs-code]: https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-aks-tools
[preview-terms]: https://azure.microsoft.com/support/legal/preview-supplemental-terms/
[supported-regions]: https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service
[troubleshooting]: /azure/dev-spaces/troubleshooting#fail-to-restore-original-configuration-of-deployment-on-cluster
[vs-code]: https://code.visualstudio.com/download
[kubernetesLocalProcessConfig-yaml]: configure-bridge-to-kubernetes.md
[btk-how-it-works]: overview-bridge-to-kubernetes.md
[btk-overview-routing]: overview-bridge-to-kubernetes.md#using-routing-capabilities-for-developing-in-isolation
