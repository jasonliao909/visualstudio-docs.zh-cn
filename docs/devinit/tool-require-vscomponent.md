---
title: require-vscomponent
description: devinit 工具 require-vscomponent。
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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`require-vscomponent` 工具用于将 Visual Studio 配置导入现有 Visual Studio。 有关 `.vsconfig` 的详细信息，请参阅[此处](../install/import-export-installation-configurations.md)。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性被省略或为空，则该工具将遵循下面详述的[默认](#default-behavior)行为。

| 名称                                     | 类型   | 必须 | 值                                                                |
|------------------------------------------|--------|----------|----------------------------------------------------------------------|
| **注释**                             | 字符串型 | 否       | 可选注释属性。 未使用。                                |
| [input](#input)                      | 字符串型 | 否       | `.vsconfig` 的完整路径。 有关详细信息，请参阅下方的 [input](#input)。 |
| [additionalOptions](#additional-options) | 字符串型 | 否       | 有关详细信息，请参阅下方的[其他选项](#additional-options)。     |

### <a name="input"></a>输入

`input` 属性用于指定 `.vsconfig` 文件的完整路径。 如果未提及，此工具将在当前目录中搜索 `.vsconfig`，并将值传递给 Visual Studio 安装程序。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为 `additionalOptions` 的值传入。 

| 名称                      | 类型      | 必须 | 值                                                                                                                                                                                    |
|---------------------------|-----------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --installPath             | 字符串型    | 否       | 要修改的 Visual Studio 实例的安装路径。                                                                                                                       |

如果没有指定安装路径，则在计算机上存在多个实例时，该工具将修改计算机上最早安装的 Visual Studio。 

### <a name="default-behavior"></a>默认行为

`require-vscomponent` 工具的默认行为是查找当前目录中的 `.vsconfig` 文件，并使用这些详细信息在静默模式下运行 Visual Studio 安装程序。 `require-vscomponent` 仅支持修改现有 Visual Studio 安装。 

## <a name="example-usage"></a>用法示例
下面是一个有关如何使用 `.devinit.json` 运行 `require-vscomponent` 的示例。

#### <a name="devinitjson-that-will-import-the-configurations-of-a-given-vsconfig-file-path"></a>用于导入给定的 .vsconfig 文件路径配置的 .devinit.json：
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

#### <a name="devinitjson-that-will-import-the-configurations-of-a-given-vsconfig-file-path-to-the-visual-studio-instance-specified-via-an-install-path"></a>用于将给定的 .vsconfig 文件路径的配置导入到通过安装路径指定的 Visual Studio 实例的 .devinit.json：
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