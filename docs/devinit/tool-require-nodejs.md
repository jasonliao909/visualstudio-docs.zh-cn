---
title: require-nodejs
description: devinit 工具需要-nodejs。
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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该 `require-nodejs` 工具用于通过 Node.js 组织分发的 MSI 来安装 [Node.js](https://nodejs.org/) 。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性均省略或为空，则该工具将遵循下面详细说明的 [默认](#default-behavior) 行为。

| 名称                                             | 类型   | 必须 | 值                                                                     |
|--------------------------------------------------|--------|----------|---------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                     |
| [**送**](#input)                              | 字符串型 | 否       | 要安装的 Node.JS 的版本。 有关详细信息，请参阅以下 [输入](#input) 。 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息，请参阅下面的 [其他选项](#additional-options) 。          |

### <a name="input"></a>输入

`input`属性用于指定 Node.js 版本。 可以在 [Node.js 下载页面](https://nodejs.org/en/download/)上找到版本列表。 完整版本号是必需的 (例如，14.4.0) 如果省略，则安装将失败。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为的值传入 `additionalOptions` 。 这些自变量直接传递到 MSI 安装程序以实现 Node.js。  

### <a name="default-behavior"></a>默认行为

此工具的默认行为 `require-nodejs` 是安装 Node.JS [网站](https://nodejs.org/en/download/)上详细说明的最新 LTS 版本的节点。

## <a name="example-usage"></a>用法示例
下面是如何使用运行的示例 `require-nodejs` `.devinit.json` 。 

#### <a name="devinitjson-that-will-install-the-lts-of-nodejs"></a>devinit 将安装的 LTS Node.js：
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

#### <a name="devinitjson-that-will-install-a-specific-version-of-nodejs"></a>devinit，它将安装 Node.js 的特定版本：
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
