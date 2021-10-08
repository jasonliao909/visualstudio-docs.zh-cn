---
title: 在 Linux 中使用 WSL 调试 .NET 应用
description: 了解如何在不离开 Visual Studio 的情况下，在 WSL 中运行和调试 .NET 应用。
ms.date: 09/17/2021
ms.topic: conceptual
helpviewer_keywords:
- debugging, linux
- debugging, wsl2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: 1ab2f44a0def0f5b766004a199c17d23ff697920
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128427286"
---
# <a name="debug-net-apps-in-wsl-with-visual-studio"></a>使用 Visual Studio 在 WSL 中调试 .NET 应用

在不离开 Visual Studio 的情况下，可以使用 WSL 轻松地在 Linux 中运行和调试 .NET 应用。 如果你是跨平台开发人员，可将此方法用作一种用来测试更多目标环境的简单方法。

对于面向 Linux 的 Windows .NET 用户，WSL 在生产现实性和工作效率之间处于最有效的位置。 在 Visual Studio 中，你已经可以使用[远程调试器](../debugger/remote-debugging-dotnet-core-linux-with-ssh.md)在远程 Linux 环境中进行调试，或者使用[容器工具](../containers/overview.md)在容器中进行调试。 当生产现实性是你主要关注的问题时，应使用这些选项之一。 当一个简单而快速的内部循环更重要时，WSL 是一个不错的选择。

不需要只选择一种方法！ 你可在同一个项目中为 Docker 和 WSL 创建启动配置文件，然后针对特定的运行操作，选择其中一个适合的配置文件即可。 部署应用后，如果出现问题，你始终可使用远程调试器附加到该应用。

>[!NOTE]
> 从 Visual Studio 2019 版本 16.11 预览版 3 开始，WSL 2 调试目标已重命名为 WSL。

## <a name="prerequisites"></a>必备条件

- Visual Studio 2019 v16.9 预览版 1 或更高版本（通过 WSL 可选组件进行 .NET 调试）。

  若要检查 WSL 组件，请选择“工具” > “获取工具和功能” 。 在 Visual Studio 安装程序中，请确保通过选择“单个组件”选项卡，然后键入“WSL”作为搜索词来安装组件 。

  在某些版本的 Visual Studio 中，默认情况下会在某些 .NET 工作负载中包含可选组件。

- 安装 [WSL](/windows/wsl/about)。

- 安装所选的[分发版](https://aka.ms/wslstore)。

## <a name="start-debugging-with-wsl"></a>通过 WSL 开始调试

1. 安装所需的组件后，在 Visual Studio 中打开一个 ASP.NET Core Web 应用或 .NET Core 控制台应用。你将看到一个名为 WSL 的新启动配置文件：

   ![启动配置文件列表中的 WSL 启动配置文件](media/linux-wsl2-debugging-select-launch-profile.png)

1. 选择此配置文件，将其添加到 launchSettings.json。

   以下示例显示了该文件中的一些主要属性。

    ::: moniker range=">=vs-2022"

    >[!NOTE]
    > 从 Visual Studio 2022 预览版 3 开始，启动配置文件中的命令名称从 WSL2 更改为 WSL。

    ```json
    "WSL": {
        "commandName": "WSL",
        "launchBrowser": true,
        "launchUrl": "https://localhost:5001",
        "environmentVariables": {
            "ASPNETCORE_URLS": "https://localhost:5001;http://localhost:5000",
            "ASPNETCORE_ENVIRONMENT": "Development"
        },
        "distributionName": ""
    }
    ```
    ::: moniker-end
    ::: moniker range="vs-2019"
    ```json
    "WSL": {
        "commandName": "WSL2",
        "launchBrowser": true,
        "launchUrl": "https://localhost:5001",
        "environmentVariables": {
            "ASPNETCORE_URLS": "https://localhost:5001;http://localhost:5000",
            "ASPNETCORE_ENVIRONMENT": "Development"
        },
        "distributionName": ""
    }
    ```
    ::: moniker-end

   选择新的配置文件后，扩展会检查 WSL 分发版是否已为运行 .NET 应用进行了配置，并帮助你安装任何缺少的依赖项。 安装这些依赖项后，即可在 WSL 中进行调试。

1. 正常开始调试，你的应用将在默认的 WSL 分发版中运行。

   要验证你是否在 Linux 中运行，一种简单的方法是检查 `Environment.OSVersion` 的值。

>[!NOTE]
> 只有 Ubuntu 和 Debian 经过了测试且受支持。 .NET 支持的其他分发版应可正常工作，但要求手动安装 [.NET 运行时](https://aka.ms/wsldotnet)和 [Curl](https://curl.haxx.se/)。

## <a name="choose-a-specific-distribution"></a>选择特定的分发版

默认情况下，WSL 2 启动配置文件使用 wsl.exe 中设置的默认分发版。 如果希望启动配置文件以特定的分发版为目标，而不考虑默认设置，则可修改启动配置文件。 例如，如果你要调试一个 Web 应用，并希望在 Ubuntu 20.04 上对其进行测试，则启动配置文件应如下所示：

::: moniker range=">=vs-2022"
```json
"WSL": {
    "commandName": "WSL",
    "launchBrowser": true,
    "launchUrl": "https://localhost:5001",
    "environmentVariables": {
        "ASPNETCORE_URLS": "https://localhost:5001;http://localhost:5000",
        "ASPNETCORE_ENVIRONMENT": "Development"
    },
    "distributionName": "Ubuntu-20.04"
}
```
::: moniker-end
::: moniker range="vs-2019"
```json
"WSL": {
    "commandName": "WSL2",
    "launchBrowser": true,
    "launchUrl": "https://localhost:5001",
    "environmentVariables": {
        "ASPNETCORE_URLS": "https://localhost:5001;http://localhost:5000",
        "ASPNETCORE_ENVIRONMENT": "Development"
    },
    "distributionName": "Ubuntu-20.04"
}
```
::: moniker-end

## <a name="target-multiple-distributions"></a>以多个分发版为目标

再深入一步，如果你要处理一个需要在多个分发版中运行的应用程序，并且希望快速地在每个分发版上测试该应用程序，可创建多个启动配置文件。 例如，如果需要在 Debian、Ubuntu 18.04 和 Ubuntu 20.04 上测试控制台应用，可使用以下启动配置文件：

::: moniker range=">=vs-2022"
```json
"WSL : Debian": {
    "commandName": "WSL",
    "distributionName": "Debian"
},
"WSL : Ubuntu 18.04": {
    "commandName": "WSL",
    "distributionName": "Ubuntu-18.04"
},
"WSL : Ubuntu 20.04": {
    "commandName": "WSL",
    "distributionName": "Ubuntu-20.04"
}
```
::: moniker-end
::: moniker range="vs-2019"
```json
"WSL : Debian": {
    "commandName": "WSL2",
    "distributionName": "Debian"
},
"WSL : Ubuntu 18.04": {
    "commandName": "WSL2",
    "distributionName": "Ubuntu-18.04"
},
"WSL : Ubuntu 20.04": {
    "commandName": "WSL2",
    "distributionName": "Ubuntu-20.04"
}
```
::: moniker-end

通过这些启动配置文件，可轻松地在各个目标分发版之间来回切换，且均无需离开 Visual Studio。

![启动配置文件列表中的多个 WSL 启动配置文件](media/linux-wsl2-debugging-switch-target-distribution.png)

## <a name="wsl-settings-in-the-launch-profile"></a>启动配置文件中的 WSL 设置

下表显示了启动配置文件中支持的设置。

|名称|默认|目的|支持令牌？|
|-|-|-|-|
|executablePath|dotnet|要运行的可执行文件|是|
|commandLineArgs|映射到 WSL 环境的 MSBuild 属性 TargetPath 的值|传递到 executablePath 的命令行参数|是|
|workingDirectory|对于控制台应用：{OutDir}</br>对于 Web 应用：{ProjectDir}|在其中开始调试的工作目录|是|
|environmentVariables||要为已调试进程设置的环境变量的键值对。|是|
|setupScriptPath||要在调试前运行的脚本。 适用于运行 ~/.bash_profile 等脚本。|是|
|distributionName||要使用的 WSL 分发版的名称。|否|
|launchBrowser|false|是否启动浏览器|否|
|launchUrl||launchBrowser 为 true 时要启动的 URL|否|

支持的令牌：

{ProjectDir} - 项目目录的完整路径

{OutDir} - MSBuild 属性 `OutDir` 的值

>[!NOTE]
> 所有路径均适用于 WSL 而非 Windows。
