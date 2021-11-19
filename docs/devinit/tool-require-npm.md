---
title: require-npm
description: devinit 工具 require-npm。
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
ms.openlocfilehash: 93723ee50fd718c5abb7c86f0f3b986ed9832abd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832968"
---
# <a name="require-npm"></a>require-npm

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`require-npm` 工具用来安装 [NPM](https://www.npmjs.com/)。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性被省略或为空，则该工具将遵循下面详述的[默认](#default-behavior)行为。

| 名称                                             | 类型   | 必须 | 值                                                                                       |
|--------------------------------------------------|--------|----------|---------------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                                       |
| [input](#input)                              | 字符串 | 是      | 指定 NPM 版本。 有关详细信息，请参阅下方的 [Input](#input)。                           |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 未使用。 有关详细信息，请参阅下方的[其他选项](#additional-options)。                  |

### <a name="input"></a>输入

`input` 属性用于指定 npm 版本。

### <a name="additional-options"></a>附加选项

未使用。

### <a name="default-behavior"></a>默认行为

`require-nodejs` 工具的默认行为是安装 npm 的最新 LTS 版本。

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `require-npm` 的示例。

#### <a name="devinitjson-that-will-install-the-lts-of-npm"></a>将安装 npm 的 LTS 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-npm"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-npm"></a>将安装特定版本 npm 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-npm",
            "input": "6.14.6"
        }
    ]
}
```