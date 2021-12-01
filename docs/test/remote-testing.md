---
title: Visual Studio 中的远程测试
description: 了解如何使用 Visual Studio 测试资源管理器中的远程测试功能来从远程环境（包括容器、WSL2 或通过 SSH 连接）运行测试。 本主题介绍如何使用 testenvironments.json 来针对本地容器、WSL2 或 SSH 连接配置远程测试。
ms.date: 08/26/2021
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
monikerRange: '>= vs-2022'
ms.workload:
- multiple
ms.openlocfilehash: 7b756ac42a7747d1d9011b5e3e84f75731b38a7e
ms.sourcegitcommit: 263703af9c4840e0e0876aa99df6dd7455c43519
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2021
ms.locfileid: "133387476"
---
# <a name="remote-testing-experimental-preview"></a>远程测试（试验性预览）

通过远程测试，开发人员可将 Visual Studio 2022 连接到远程环境来运行和调试测试。 如果有跨平台开发人员在将代码部署到多个不同的目标环境中，例如不同的 Windows 或 Linux 操作系统，那么他们适合使用此使用。 例如，开发人员通常必须将更改推送到 CI 管道，才能从 Linux 上运行的测试获取反馈。 而有了此功能，你可将测试资源管理器连接到远程环境，直接从 Visual Studio 运行 Linux 测试。

关于使用此试验版远程测试的要求：
* Visual Studio 2022 Update 17.0 预览版 3 或更高版本
* 仅适用于 .NET 测试。
  * 如果你有兴趣了解对其他语言的远程测试支持，请[提交建议](/visualstudio/ide/suggest-a-feature)或投票支持现有建议。 [支持 C++ 远程测试](https://developercommunity.visualstudio.com/t/run-c-unit-tests-on-linux-with-visual-studio/1403357)。
* 目前，我们只支持远程环境中的 Windows、Ubuntu 和 Debian 映像。 
* 目前，环境的大部分预配由用户的规范决定。 用户必须在你的目标环境中安装必需的依赖项。 例如，如果测试面向 .NET 6.0，则需要确保容器已通过 Dockerfile 安装了 .NET 6.0。 可能会有提示在远程环境中安装 .NET Core，这是远程运行和发现测试所必需的。 
* 通过“输出”>“测试”窗格，规划监视到远程环境的连接状态。 例如，如果已停止容器，“输出”>“测试”窗格中会显示一条消息。 我们可能不会检测到所有的情况，因此如果看起来像断开了连接，请计划检查你的输出。 特别是在“输出”窗格未设置为“测试”的情况下，你可能不会立即看到消息。 如果断开了连接，你可使用测试资源管理器中的环境下拉菜单将连接设置回本地环境，然后再次选择远程环境来重新启动连接。

## <a name="set-up-the-remote-testing-environment"></a>设置远程测试环境

在解决方案的根目录中使用 `testenvironments.json` 指定环境。 JSON 文件结构遵循下述架构：
```json
{
    "version": "1", // value must be 1
    "environments": [
        { "name": "<unique name>", ... },
        ...
    ]
}
```

### <a name="local-container-connections"></a>本地容器连接

若要连接到本地运行的容器，必须在本地计算机上安装 [Docker 桌面](https://www.docker.com/products/docker-desktop)。 还可以选择[启用 WSL2 集成](/windows/wsl/install-win10)，以获得更好的性能。

对于 Dockerfile，可在解决方案的根目录中使用 `testEnvironments.json` 指定环境。 它使用此处所述的属性。
```json
    {
    "name": "<name>",
    "localRoot": "<path to local environment>", // optional
    "type": "docker",
    "dockerImage": "<docker image tag>",
    }
```

对于名为 \<mcr.microsoft.com/dotnet/core/sdk\> 的本地容器映像，以下示例显示 `testenvironments.json`。
```json
{
"version": "1",
"environments": [
    {
    "name": "linux dotnet-core-sdk-3.1",
    "type": "docker",
    "dockerImage": "mcr.microsoft.com/dotnet/core/sdk"
    }
]
}
```

下面的示例演示了一个 Dockerfile，它用于运行面向 .NET 5.0 的测试。 第二行确保调试程序可在容器中连接并运行。
```
FROM mcr.microsoft.com/dotnet/core/sdk:5.0

RUN wget https://aka.ms/getvsdbgsh && \
    sh getvsdbgsh -v latest  -l /vsdbg
```

该容器必须在本地计算机上具有生成的映像。 你可使用以下命令生成容器（在末尾加上“.”）：`docker build -t <docker image name> -f <path to Dockerfile> .`

### <a name="local-wsl2-connections"></a>本地 WSL2 连接
若要在 WSL2 上远程运行测试，必须在本地计算机上[启用 WSL2 集成](/windows/wsl/install-win10)。

可使用以下架构，并将 \<Ubuntu\> 替换为你安装的 WSL2 发行版，在解决方案的根目录中使用 `testEnvironments.json` 指定环境。
```json
{
"version": "1",
"environments": [
    {
    "name": "WSL-Ubuntu",
    "type": "wsl",
    "wslDistribution": "Ubuntu"
    }
]
}
```

### <a name="ssh-connections"></a>SSH 连接
 可通过“工具”>“选项”>“跨平台”>“连接管理器”，来添加或删除 SSH 连接。 选择“添加”将可以输入所需的主机名、端口和任何凭据。

可使用以下架构，并将 `\<ssh://user@hostname:22\>` 替换为你的 SSH remoteUri，在解决方案的根目录中使用 `testEnvironments.json` 指定环境。
```json
{
"version": "1",
"environments": [
    {
    "name": "ssh-remote",
    "type": "ssh",
    "remoteUri": "ssh://user@hostname:22"
    }
]
}
```

#### <a name="prerequisites-for-a-remote-windows-environment"></a>远程 Windows 环境的先决条件
1. 确保已启用 [Windows Projected File System](/windows/win32/projfs/enabling-windows-projected-file-system)。 可以从管理员 PowerShell 窗口运行以下命令来启用它：

   ```powershell
    Enable-WindowsOptionalFeature -Online -FeatureName Client-ProjFS -NoRestart
   ```

   如果需要，请重新启动环境。
2. 确保已设置 SSH。 可以在[安装 OpenSSH](/windows-server/administration/openssh/openssh_install_firstuse#install-openssh-using-powershell) 中查看这些步骤。 从管理员 PowerShell 窗口运行以下命令来启动 SSH 服务器：
   ```powershell
   Start-Service sshd
   ```

3. 确保安装了测试所需的相应 .NET 运行时。 可在[此处](https://dotnet.microsoft.com/download)找到下载。
4. 用于调试测试：
   1. 请在远程环境中安装[远程工具 SKU](/visualstudio/debugger/remote-debugging?view=vs-2022&preserve-view=true)。 
   2. 以管理员身份启动远程调试器，并确保 VS 用户具有连接权限。

#### <a name="prerequisites-for-a-remote-linux-environment"></a>远程 Linux 环境的先决条件
1. 确保 SSH 已配置且正在运行。
2. 使用包管理器安装 `fuse3`。
3. 确保在远程环境中安装了测试所需的相应 .NET 运行时。

## <a name="use-the-test-explorer-to-run-and-debug-remote-tests"></a>使用测试资源管理器运行和调试远程测试
* 通过测试资源管理器工具栏中的下拉菜单选择处于活动状态的环境。 目前，一次只能有一个测试环境处于活动状态。

  ![“测试资源管理器”中的远程测试环境下拉菜单](media/remote-test-drop-down.png)

* 选择环境后，将在新环境中发现并运行测试。

  ![在远程环境中发现并执行测试](media/remote-test-linux-discovery.png)

* 现在远程运行测试，并在环境中调试测试！

  ![在“测试资源管理器”中查看远程环境中的测试结果](media/remote-test-linux-passing.png)

* 测试资源管理器可能会提示你安装一些缺少的环境必备项，并尝试安装缺少的依赖项。 不过，远程环境的大部分预配取决于用户的规范。

## <a name="see-also"></a>请参阅

- [使用测试资源管理器调试单元测试](../test/debug-unit-tests-with-test-explorer.md)
- [将单元测试作为 64 位进程运行](../test/run-a-unit-test-as-a-64-bit-process.md)
- [测试资源管理器常见问题解答](test-explorer-faq.md)
