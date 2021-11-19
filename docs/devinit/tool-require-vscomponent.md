---
title: require-vscomponent
description: devinit 工具需要-vscomponent。
ms.date: 02/08/2021
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 7d6609c49efb9f77c9823ca3f703b8843ddb753e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833108"
---
# <a name="require-vscomponent"></a>require-vscomponent

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该 `require-vscomponent` 工具用于将 Visual Studio 配置导入现有 Visual Studio。 了解更多 `.vsconfig` [相关信息](../install/import-export-installation-configurations.md)。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性均省略或为空，则该工具将遵循下面详细说明的 [默认](#default-behavior) 行为。

| 名称                                     | 类型   | 必须 | 值                                                                |
|------------------------------------------|--------|----------|----------------------------------------------------------------------|
| **注释**                             | 字符串型 | 否       | 可选注释属性。 未使用。                                |
| [**送**](#input)                      | 字符串型 | 否       | 的完整路径 `.vsconfig` 。 有关详细信息，请参阅以下 [输入](#input) 。 |
| [additionalOptions](#additional-options) | 字符串型 | 否       | 有关详细信息，请参阅下面的 [其他选项](#additional-options) 。     |

### <a name="input"></a>输入

`input`属性用于指定文件的完整路径 `.vsconfig` 。 如果未提到，此工具将 `.vsconfig` 在当前目录中搜索，并将值传递给 Visual Studio 安装程序。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为的值传入 `additionalOptions` 。 

| 名称                      | 类型      | 必须 | 值                                                                                                                                                                                    |
|---------------------------|-----------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --installPath             | 字符串型    | 否       | 要修改的 Visual Studio 实例的安装路径。                                                                                                                       |

如果未指定安装路径，则在计算机上存在多个实例时，该工具将修改计算机上安装的最早 Visual Studio。 

### <a name="default-behavior"></a>默认行为

此工具的默认行为 `require-vscomponent` 是查找 `.vsconfig` 当前目录中的文件，并使用这些详细信息在安静模式下运行 Visual Studio 安装程序。 `require-vscomponent`仅支持修改现有 Visual Studio 安装。 

## <a name="example-usage"></a>用法示例
下面是如何使用运行的示例 `require-vscomponent` `.devinit.json` 。

#### <a name="devinitjson-that-will-import-the-configurations-of-a-given-vsconfig-file-path"></a>devinit，它将导入 vsconfig 文件路径的配置：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "comments": "A sample dot-devinit file.",
    "run": [
        {
            "tool": "require-vscomponent",
            "input": "C:\\.vsconfig"
        }
    ]
}
```

#### <a name="devinitjson-that-will-import-the-configurations-of-a-given-vsconfig-file-path-to-the-visual-studio-instance-specified-via-an-install-path"></a>devinit，用于将给定. vsconfig 文件路径的配置导入通过安装路径指定的 Visual Studio 实例：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "comments": "A sample dot-devinit file.",
    "run": [
        {
            "tool": "require-vscomponent",
            "input": "C:\\.vsconfig",
            "additionalOptions": "--installPath 'C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\Enterprise'"
        }
    ]
}
```