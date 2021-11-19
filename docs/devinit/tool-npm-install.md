---
title: npm-install
description: devinit 工具 npm-install。
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
ms.openlocfilehash: 011364e851670362ecaa9f4bdbfff965782ed706
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832989"
---
# <a name="npm-install"></a>npm-install

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`npm-install` 工具可以用来安装 [NPM](https://www.npmjs.com/) 包。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性被省略或为空，则该工具将不执行任何操作。

| 名称                                             | 类型   | 必须 | 值                                                                                                          |
|--------------------------------------------------|--------|----------|----------------------------------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                                                          |
| [input](#input)                              | 字符串型 | 否       | 要安装的程序包。 有关详细信息，请参阅下方的 [Input](#input)。                                                 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 要传递给该工具的其他选项。 有关详细信息，请参阅下方的[其他选项](#additional-options)。       |

### <a name="input"></a>输入

`input` 属性用于指定要安装的包的名称（例如“mongo”）。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为 `additionalOptions` 的值传入。 这些参数直接传递到由 [npm install](https://docs.npmjs.com/cli/install) 使用的参数。

### <a name="default-behavior"></a>默认行为

`npm-install` 工具的默认行为是在没有参数的情况下运行 `npm install`。 有关此行为的说明，请参阅 [npm 文档](https://docs.npmjs.com/cli/v6/commands/npm-install)。

## <a name="example-usage"></a>用法示例
下面是一个有关如何使用 `.devinit.json` 运行 `npm-install` 的示例。

#### <a name="devinitjson-that-will-install-mongo"></a>将安装 mongo 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "npm-install",
            "input": "mongo",
        }
    ]
}
```
