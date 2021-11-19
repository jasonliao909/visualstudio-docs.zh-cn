---
title: dotnet-toolinstall
description: devinit 工具 dotnet-toolinstall。
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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该 `dotnet-toolinstall` 工具用于通过命令安装 [.Net Core 工具](https://dotnet.microsoft.com/) `dotnet tool update` 。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性均省略或为空，则该工具将遵循下面详细说明的 [默认](#default-behavior) 行为。

| 名称                                             | 类型   | 必须 | 值                                                                 |
|--------------------------------------------------|--------|----------|-----------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                 |
| [**送**](#input)                              | 字符串 | 是      | 要安装的 .NET Core 工具。 有关详细信息，请参阅以下 [输入](#input) 。 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息，请参阅下面的 [其他选项](#additional-options) 。      |

### <a name="input"></a>输入

`input`属性用于指定要安装的 .Net Core 工具。 中有一个非正式工具列表 [https://github.com/natemcmaster/dotnet-tools](https://github.com/natemcmaster/dotnet-tools) 。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为的值传入 `additionalOptions` 。 这些自变量直接传递给命令使用的参数 [`dotnet tool update`](/dotnet/core/tools/global-tools#update-a-tool) 。

`dotnet tool update`命令用于安全地处理已安装工具的情况。

### <a name="default-behavior"></a>默认行为

此工具的默认行为 `dotnet-toolinstall` 是 "需要时出错" `input` 。

## <a name="example-usage"></a>用法示例
下面是如何使用运行的示例 `dotnet-toolinstall` `.devinit.json` 。

#### <a name="devinitjson-that-will-install-the-dotnet-trace-tool"></a>要安装 dotnet 工具的 devinit：
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

#### <a name="devinitjson-that-will-install-the-dotnet-trace-tool-as-a-global-tool"></a>devinit，它将 dotnet 工具作为全局工具安装：
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