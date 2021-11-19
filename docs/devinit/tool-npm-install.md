---
title: npm-install
description: devinit 工具 npm-安装。
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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该 `npm-install` 工具可用于安装 [NPM](https://www.npmjs.com/) 包。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性均省略或为空，则该工具将不执行任何操作。

| 名称                                             | 类型   | 必须 | 值                                                                                                          |
|--------------------------------------------------|--------|----------|----------------------------------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                                                          |
| [**送**](#input)                              | 字符串型 | 否       | 要安装的程序包。 有关详细信息，请参阅以下 [输入](#input) 。                                                 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 要传递给该工具的其他选项。 有关详细信息，请参阅下面的 [其他选项](#additional-options) 。       |

### <a name="input"></a>输入

`input`属性用于指定要安装的包的名称 (例如 "mongo" ) 。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为的值传入 `additionalOptions` 。 这些参数直接传递到 [npm install](https://docs.npmjs.com/cli/install)使用的参数。

### <a name="default-behavior"></a>默认行为

此工具的默认行为 `npm-install` 是在没有参数的情况下运行 `npm install` 。 有关此行为的说明，请参阅 [npm 文档](https://docs.npmjs.com/cli/v6/commands/npm-install) 。

## <a name="example-usage"></a>用法示例
下面是如何使用运行的示例 `npm-install` `.devinit.json` 。

#### <a name="devinitjson-that-will-install-mongo"></a>devinit 将安装 mongo 的：
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
