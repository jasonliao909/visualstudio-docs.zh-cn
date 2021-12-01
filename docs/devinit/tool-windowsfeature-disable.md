---
title: windowsfeature-disable
description: devinit tool windowsfeature-disable。
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
ms.openlocfilehash: cd06b3a3d063a2c209a901bbed1600570c31cd8e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832974"
---
# <a name="windowsfeature-disable"></a>windowsfeature-disable

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该 `windowsfeature-disable` 工具用于获取 Windows 功能。

## <a name="usage"></a>使用情况

| 名称                                             | 类型   | 必须 | 值                                                                  |
|--------------------------------------------------|--------|----------|------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                  |
| [input](#input)                              | 字符串 | 是      | 要安装的 Windows 功能。 有关详细信息，请参阅下方的 [Input](#input)。 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息，请参阅下方的[其他选项](#additional-options)。       |

### <a name="input"></a>输入

`input` 属性应该是要禁用的 `windows feature` 的 `name`。

### <a name="additional-options"></a>Additional-Options

无。

### <a name="default-behavior"></a>默认行为

该 `windowsfeature-disable` 工具的默认行为出错，因为需要 `input`。

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `windowsfeature-disable` 的示例。

#### <a name="devinitjson-that-will-disable-a-specified-feature"></a>.devinit.json 将禁用指定功能：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-windowsfeature",
            "input": "web-server",
        }
    ]
}
```
