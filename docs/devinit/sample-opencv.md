---
title: OpenCV
description: 使用 devinit 面向 OpenCV 存储库的 Linux 和 Windows 的示例自定义。
ms.date: 08/28/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 319f560e4661f12acbef941692e5fd2c257c25ee
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833027"
---
# <a name="opencv"></a>OpenCV

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

此示例说明了如何自定义 [GitHub Codespaces](https://github.com/features/codespaces)，以便使用 [opencv/OpenCV](https://github.com/opencv/opencv) 等多平台项目进行开发。

以下自定义项已应用于分支 [microsoft/OpenCV](https://github.com/microsoft/opencv)，并允许面向 Windows 和 Ubuntu 生成。

## <a name="customization-with-devcontainerjson-and-devinitjson"></a>使用 devcontainer.json 和 devinit.json 进行自定义

`.devcontainer` 目录需要包含以下文件：

* devcontainer.json
* devinit.json

### <a name="devcontainerjson"></a>devcontainer.json

以下是 devcontainer.json 文件的内容。

```json
{
  "postCreateCommand": "devinit init"
}
```

`postCreateCommand` 启动 [devinit](devinit-and-codespaces.md) 工具，该工具使用 devinit.json。

### <a name="devinitjson"></a>devinit.json

以下是 [devinit.json](devinit-json.md) 文件的内容。

```json
{
    "run": [
        {
            "comments": "Example that will install Ubuntu 20.04 using WSL2, and configure it with various packages useful for C++ development.",
            "tool": "wsl-install",
            "input": "https://aka.ms/wslubuntu2004",
            "additionalOptions": "--wsl-version 2 --post-create-command 'apt-get update && apt-get install g++ gcc g++-9 gcc-9 cmake gdb ninja-build zip rsync -y'"
        }
    ]
}
```

devinit.json 是 [devinit](devinit-and-codespaces.md) 工具使用的文件，它必须与 devcontainer.json 位于同一目录中。

在此示例中，[wsl-install](tool-wsl-install.md) 工具用于创建一个运行 Ubuntu 20.04 的 WSL 实例，并使用基本 C++ 开发工具对其进行预配。
## <a name="targeting-windows-or-linux"></a>面向 Windows 或 Linux

始终创建名为 `x64-Debug` 的面向 Windows 的默认生成配置。

通过添加上述文件，在创建 Codespace 实例时，Visual Studio 会在[连接管理器](/cpp/linux/connect-to-your-remote-linux-computer)中预配一个新的 SSH 连接，并在配置选取器中创建一个通过 SSH 连接面向 Ubuntu 实例的新配置。

![面向 Ubuntu 的配置](media/wsl-ssh-linux-configuration.png).

通过选择面向 WSL 的突出显示配置，可以生成和调试 OpenCV 的生成目标。
