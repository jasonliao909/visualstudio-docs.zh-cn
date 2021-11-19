---
title: nuget-restore
description: devinit 工具 nuget-还原。
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
ms.openlocfilehash: 4fe78f33533931f91e97c61ec093602ee0071895
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832985"
---
# <a name="nuget-restore"></a>nuget-restore

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该 `nuget-restore` 工具还原项目文件中指定的依赖项和特定于项目的工具。 [在此处](/nuget/reference/cli-reference/cli-ref-restore)了解 NuGet 还原的详细信息。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性均省略或为空，则该工具将遵循下面详细说明的 [默认](#default-behavior) 行为。

| 名称                                             | 类型   | 必须 | 值                                                                                |
|--------------------------------------------------|--------|----------|--------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                                |
| [**送**](#input)                              | 字符串型 | 否       | 要还原的项目/解决方案文件的路径。 有关详细信息，请参阅以下 [输入](#input) 。 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息，请参阅下面的 [其他选项](#additional-options) 。                     |

### <a name="input"></a>输入

要还原的项目/解决方案文件的路径。

### <a name="additional-options"></a>附加选项

其他选项按原样传递到 NuGet restore 命令。

### <a name="default-behavior"></a>默认行为

此工具的默认行为 `nuget-restore` 是 `NuGet restore` 在当前目录中运行。

## <a name="example-usage"></a>用法示例
下面是如何使用运行的示例 `nuget-restore` `.devinit.json` 。

#### <a name="devinitjson-that-will-restore-dependencies-and-tools-of-a-project"></a>devinit，它将还原项目的依赖项和工具：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "nuget-restore",
            "input": "C:\\nuget\\Nuget.config"
        }
    ]
}
```