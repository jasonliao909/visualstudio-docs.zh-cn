---
title: .NET Core 运行时
description: 针对 dotnet/运行时存储库使用 devinit 的示例自定义。
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
ms.openlocfilehash: d703e71b6f8ab57ab07c4143fdd5435585c6004c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833030"
---
# <a name="net-core-runtime"></a>.NET Core 运行时

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

此示例演示如何自定义 .net Core 运行时[dotnet/运行时](https://github.com/dotnet/runtime)，以自动通过[GitHub Codespaces](https://github.com/features/codespaces)进行设置。

## <a name="postclonesetupps1"></a>PostCloneSetup.ps1

此脚本从 _PostCloneSetup.ps1_ 调用，也可以在本地运行以设置存储库。 该文件需要与 .devcontainer.json 位于相同的文件夹中。

```console
devinit init
git config --system core.longpaths true
```

## <a name="packagesconfig"></a>packages.config

_packages.config_ 文件是一个 [Chocolatey](https://chocolatey.org/)文件，用于定义要安装的 Chocolatey 包的列表。 该文件需要与 .devcontainer.json 位于相同的文件夹中。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="python" version="3.8.3"  />
    <package id="cmake" version="3.17.3"  />
</packages>
```

## <a name="devinitjson"></a>.devinit.json

文件的内容 [`.devinit.json`](devinit-json.md) 。 此文件需要与 _devcontainer_ 文件位于同一文件夹中。

```json
{
    "run": [
        {
            "tool": "require-dotnetcoresdk"
        },
        {
            "tool": "choco-install",
            "input": "packages.config"
        },
        {
            "tool": "require-vscomponent"
        }
    ]
}
```

## <a name="devcontainerjson"></a>。 devcontainer

存储库根中的 .devcontainer.json 文件的内容。

```json
{
  "postCreateCommand": "Powershell.exe -ExecutionPolicy unrestricted -File .\\PostCloneSetup.ps1"
}
```
