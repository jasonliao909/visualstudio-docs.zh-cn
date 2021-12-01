---
title: windowsfeature-list
description: devinit tool windowsfeature-list。
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
ms.openlocfilehash: 3225e67db734e02abce96820d44ca1515ddc348f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833100"
---
# <a name="windowsfeature-list"></a>windowsfeature-list

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该 `windowsfeature-list` 工具用于列出所有 Windows 功能的启用/禁用状态。

| 名称                                             | 类型   | 必须 | 值                                      |
|--------------------------------------------------|--------|----------|--------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。      |
| [input](#input)                              | 字符串型 | 否       | 未使用。 已忽略。                         |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 未使用。 已忽略。                         |

### <a name="input"></a>输入

未使用。 已忽略。

#### <a name="additional-options"></a>附加选项

未使用。 已忽略。

### <a name="default-behavior"></a>默认行为

该 `windowsfeature-list` 工具的默认行为用于列出所有 Windows 功能的启用/禁用状态。

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `windowsfeature-list` 的示例。

#### <a name="devinitjson-that-will-list-the-state-of-all-windows-features"></a>.devinit.json 将列出所有 Windows 功能的状态：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0.json",
    "run": [
        {
            "tool": "windowsfeature-list"
        }
    ]
}
```
