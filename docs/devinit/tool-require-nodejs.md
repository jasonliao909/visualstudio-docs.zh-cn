---
title: require-nodejs
description: devinit 工具 require-nodejs。
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
ms.openlocfilehash: 75690f85fb627140226242b476d70bfc4dac6ed2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832978"
---
# <a name="require-nodejs"></a>require-nodejs

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`require-nodejs` 工具用于通过 Node.js 组织分发的 MSI 来安装 [Node.js](https://nodejs.org/)。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性被省略或为空，则该工具将遵循下面详述的[默认](#default-behavior)行为。

| 名称                                             | 类型   | 必须 | 值                                                                     |
|--------------------------------------------------|--------|----------|---------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                     |
| [input](#input)                              | 字符串型 | 否       | 要安装的 Node.JS 的版本。 有关详细信息，请参阅下方的 [Input](#input)。 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息，请参阅下方的[其他选项](#additional-options)。          |

### <a name="input"></a>输入

`input` 属性用于指定 Node.js 版本。 可在 [Node.js 下载页](https://nodejs.org/en/download/)上找到版本列表。 需要完整的版本号“主要版本.次要版本.路径”（例如 14.4.0），如果省略任何一个，安装将失败。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为 `additionalOptions` 的值传入。 这些参数被直接传递给 Node.js 的 MSI 安装程序。  

### <a name="default-behavior"></a>默认行为

`require-nodejs` 工具的默认行为是安装 Node 的最新 LTS 版本（Node.JS [网站](https://nodejs.org/en/download/)上进行了详细说明）。

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `require-nodejs` 的示例。 

#### <a name="devinitjson-that-will-install-the-lts-of-nodejs"></a>将安装 Node.js 的 LTS 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-nodejs"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-nodejs"></a>将安装特定版本 Node.js 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-nodejs",
            "input": "14.4.0"
        }
    ]
}
```
