---
title: wsl-install
description: devinit 工具 wsl-install。
ms.date: 11/20/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 4dff121d7866918d5c30986dc9bd4c3cab039ac5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833098"
---
# <a name="wsl-install"></a>wsl-install

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`wsl-install` 工具用于安装[适用于 Linux 的 Windows 子系统](/windows/wsl/) (WSL) 的 Linux 发行版。

> [!IMPORTANT]
> `wsl-install` 工具要求在 Windows 上已启用 WSL 2。 如果由于某种原因导致 WSL 2 未启用，你可以按照 [WSL 安装文档](https://docs.microsoft.com/windows/wsl/install-win10)操作。 还可以使用 [windowsfeature-enable](tool-windowsfeature-enable.md) 工具来启用任何所需的 Windows 功能。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性被省略或为空，则该工具将遵循下面详述的[默认](#default-behavior)行为。

| 名称                                             | 类型   | 必须 | 值                                                             |
|--------------------------------------------------|--------|----------|-------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                             |
| [input](#input)                              | 字符串 | 是      | 要安装的发行版。 有关详细信息，请参阅下方的 [Input](#input)。     |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息，请参阅下方的[其他选项](#additional-options)。  |

### <a name="input"></a>输入

AppX 应用程序分发包的 URI (`.appx`) 包含要部署的发行版。 URI 必须指向一个 `.appx` 存档，该存档包含一个 `install.tar.gz`，它要么在存档根中，要么在一个内部 `.appx` 存档中。 支持的发行版示例包括：

| 分发版                          | Uri                                                           |
|---------------------------------|---------------------------------------------------------------|
| Ubuntu 20.04                    | https://aka.ms/wslubuntu2004                                  |
| Ubuntu 18.04                    | https://aka.ms/wsl-ubuntu-1804                                |
| Ubuntu 16.04                    | https://aka.ms/wsl-ubuntu-1604                                |
| Debian GNU/Linux                | https://aka.ms/wsl-debian-gnulinux                            |
| Kali Linux                      | https://aka.ms/wsl-kali-linux-new                             |
| OpenSUSE Leap 42                | https://aka.ms/wsl-opensuse-42                                |
| SUSE Linux Enterprise Server 12 | https://aka.ms/wsl-sles-12                                    |

> [!NOTE]
> ARM Linux 发行版目前在 GitHub Codespaces 中不受支持。

### <a name="additional-options"></a>附加选项

支持多个附加选项：

| 名称                      | 类型      | 必须 | 值                                                                                                                                                                                    |
|---------------------------|-----------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --wsl-version             | 字符串型    | 否       | 要使用的 WSL 版本。 默认值为 2。                                                                                                                                  |
| --post-create-command     | 字符串型    | 否       | 安装完成后要在 Linux 发行版内部执行的命令。 应将此命令格式化为一个字词，或将其括在引号中。 默认无命令。  |

### <a name="default-behavior"></a>默认行为

`wsl-install` 工具的默认行为出错，因为需要 `input` 属性，即要安装的发行版。

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `wsl-install` 的示例。

#### <a name="devinitjson-that-will-install-ubuntu-2004"></a>将安装 Ubuntu 20.04 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "wsl-install",
            "input": "https://aka.ms/wslubuntu2004"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-ubuntu-2004-and-perform-a-post-create-command"></a>将安装 Ubuntu 20.04 并执行创建后命令的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "wsl-install",
            "input": "https://aka.ms/wslubuntu2004",
            "additionalOptions": "--wsl-version 2 --post-create-command 'echo Hello from Ubuntu!'"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-ubuntu-2004-and-perform-a-post-create-command-that-configures-the-packages-listed"></a>将安装 Ubuntu 20.04 并执行创建后命令（用于配置列出的包）的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "wsl-install",
            "input": "https://aka.ms/wslubuntu2004",
            "additionalOptions": "--wsl-version 2 --post-create-command 'apt-get update && apt-get install g++ gcc g++-9 gcc-9 cmake gdb ninja-build zip rsync -y'"
        }
    ]
}
```
