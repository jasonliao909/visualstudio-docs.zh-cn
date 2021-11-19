---
title: require-nuget
description: devinit 工具需要-nuget。
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
ms.openlocfilehash: c49f77fe8b32ce6617b34d522e36cc5988d0c33c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832969"
---
# <a name="require-nuget"></a>require-nuget

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该 `require-nuget` 工具会下载 NuGet CLI 并将其添加到中 `PATH` 。 NuGetCLI 提供全部 NuGet 功能，用于安装、创建、发布和管理包，而无需对项目文件进行任何更改。 [在此处](/nuget/reference/nuget-exe-cli-reference)阅读有关 NuGet CLI 的详细信息。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性均省略或为空，则该工具将遵循下面详细说明的 [默认](#default-behavior) 行为。

| 名称                                             | 类型   | 必须 | 值                                                                                |
|--------------------------------------------------|--------|----------|--------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                                |
| [**送**](#input)                              | 字符串型 | 否       | NuGet要安装的 CLI 版本。 有关详细信息，请参阅以下 [输入](#input) 。 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息，请参阅下面的 [其他选项](#additional-options) 。                     |

### <a name="input"></a>输入

`input`是一个可选属性，用于特定于要安装 NuGet CLI 的版本。 如果 `input` 省略，将安装最新版本的 CLI。

### <a name="additional-options"></a>附加选项

未使用。

### <a name="default-behavior"></a>默认行为

此工具的默认行为 `require-nuget` 是安装最新的 NuGet CLI。

## <a name="example-usage"></a>用法示例
下面是如何使用运行的示例 `require-nuget` `.devinit.json` 。

#### <a name="devinitjson-that-will-install-a-specified-version-of-nuget"></a>devinit 将安装 NuGet 的指定版本的. json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-nuget",
            "input": "5.5.1",
        }
    ]
}
```