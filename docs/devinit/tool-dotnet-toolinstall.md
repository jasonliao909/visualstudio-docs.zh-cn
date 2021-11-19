---
title: dotnet-toolinstall
description: devinit tool dotnet-toolinstall。
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
ms.openlocfilehash: 4daa3722abd169c03656adec39aafc29d5e7e435
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832997"
---
# <a name="dotnet-toolinstall"></a>dotnet-toolinstall

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`dotnet-toolinstall` 工具用于通过 `dotnet tool update` 命令安装 [.NET Core 工具](https://dotnet.microsoft.com/)。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性省略或为空，则该工具将遵循下面详述的[默认](#default-behavior)行为。

| 名称                                             | 类型   | 必须 | 值                                                                 |
|--------------------------------------------------|--------|----------|-----------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                 |
| [input](#input)                              | 字符串 | 是      | 要安装的 .NET Core 工具。 有关详细信息，请参阅下方的 [Input](#input)。 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息，请参阅下方的[其他选项](#additional-options)。      |

### <a name="input"></a>输入

`input` 属性用于指定要安装的 .NET Core 工具。 [https://github.com/natemcmaster/dotnet-tools](https://github.com/natemcmaster/dotnet-tools) 中有一个非正式工具列表。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为 `additionalOptions` 值传入。 这些参数直接传递到由 [`dotnet tool update`](/dotnet/core/tools/global-tools#update-a-tool) 使用的参数。

`dotnet tool update` 命令用于安全地处理已安装工具的情况。

### <a name="default-behavior"></a>默认行为

该 `dotnet-toolinstall` 工具的默认行为出错，因为需要 `input`。

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `dotnet-toolinstall` 的示例。

#### <a name="devinitjson-that-will-install-the-dotnet-trace-tool"></a>要安装 dotnet-trace 工具的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "dotnet-toolinstall",
            "input": "dotnet-trace"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-the-dotnet-trace-tool-as-a-global-tool"></a>要安装 dotnet-trace 工具作为全局工具的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "dotnet-toolinstall",
            "input": "dotnet-trace",
            "additionalOptions": "--global"
        }
    ]
}
```