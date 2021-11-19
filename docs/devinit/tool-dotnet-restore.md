---
title: dotnet-restore
description: devinit 工具 dotnet-restore。
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
ms.openlocfilehash: 5beea84edce408acda7fc157f530c4a5f3253835
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832998"
---
# <a name="dotnet-restore"></a>dotnet-restore

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们专注于为云支持的内部循环和 VDI 解决方案提供不断发展的体验，这些解决方案针对一组广泛的Visual Studio工作负载进行优化。 作为此和 `devinit` 关联工具的一部分，将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`dotnet-restore`该工具还原项目文件中指定的依赖项和特定于项目的工具。 在此处详细了解[dotnet restore。](/dotnet/core/tools/dotnet-restore)

## <a name="usage"></a>使用情况

如果省略 `input` 和 属性或属性 `additionalOptions` 为空，该工具将遵循 [下面详述](#default-behavior) 的默认行为。

| 名称                                             | 类型   | 必须 | 值                                                                                |
|--------------------------------------------------|--------|----------|--------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                                |
| [**输入**](#input)                              | 字符串型 | 否       | 要还原的项目/解决方案文件的路径。 有关详细信息 [，](#input) 请参阅下面的输入。 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息 [，请参阅](#additional-options) 下面的其他选项。                     |

### <a name="input"></a>输入

要还原的项目/解决方案文件的路径。

### <a name="additional-options"></a>附加选项

其他选项将像现在一样传递到 dotnet restore 命令。

### <a name="default-behavior"></a>默认行为

该工具的默认 `dotnet-restore` 行为是在当前 `dotnet restore` 目录中运行。

## <a name="example-usage"></a>用法示例
下面是如何使用 运行 `dotnet-restore` 的示例 `.devinit.json` 。

#### <a name="devinitjson-that-will-restore-dependencies-and-tools-of-a-project"></a>将还原项目的依赖项和工具的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "dotnet-restore",
            "input": "C:\\app1\\app1.csproj"
        }
    ]
}
```