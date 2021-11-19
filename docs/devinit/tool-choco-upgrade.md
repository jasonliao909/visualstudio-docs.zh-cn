---
title: choco-upgrade
description: devinit 工具 choco 升级。
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
ms.openlocfilehash: bcd2288ef9399f27f53565ea7ea971579cad7858
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833000"
---
# <a name="choco-upgrade"></a>choco-upgrade

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`choco-upgrade` 工具可以用来安装和更新 [chocolatey](https://chocolatey.org/docs/commandsupgrade) 包。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性被省略或为空，则该工具将不执行任何操作。

| 名称                                             | 类型   | 必须  | 值                                                                                                          |
|--------------------------------------------------|--------|-----------|----------------------------------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否        | 可选注释属性。 未使用。                                                                          |
| [input](#input)                              | 字符串 | 是       | 要升级的包。 有关详细信息，请参阅下方的 [Input](#input)。                                                 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否        | 要传递给该工具的其他选项。 有关详细信息，请参阅下方的[其他选项](#additional-options)。       |

### <a name="input"></a>输入

`input` 属性用于指定要升级的包的名称（例如“mongodb”）或以下格式的配置文件路径 packages.config、.nuspec 和 .nupkg。 `input` 值将追加到 `choco upgrade` 命令（例如 `choco upgrade mongodb`），以及 [`additionalOptions`](#additional-options) 中特定的任何参数和内置 `choco` 选项（如[下面](#built-in-options)所定义的）。 包可位于 [Chocolatey 包库](https://chocolatey.org/packages)中。 使用配置文件时，可以在 `input` 属性中传递该文件的路径，例如：`"input":"packages.config"`。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为 `additionalOptions` 值传入。 这些参数直接传递到由 [`choco upgrade`](https://chocolatey.org/docs/commands-upgrade) 使用的参数并在 chocolatey 文档中定义。

### <a name="built-in-options"></a>内置选项

`choco-upgrade` 工具设置了多个 `choco` 命令行参数，以确保 `choco` 能够无外设运行。 下面列出了这些参数，相关文档可在 [chocolatey 文档](https://chocolatey.org/docs/)中找到。

| 名称                  | 说明                                                                                        |
|-----------------------|----------------------------------------------------------------------------------------------------|
| **--yes**             | 确认所有提示 - 选择肯定回答而不是提示。 意味着 `--accept-license`。 |
| --no-progress     | 不显示进度 - 不显示进度百分比。                                         |
| --skip-powershell | 跳过 PowerShell - chocolateyInstall.ps1 不会运行。                                              |

### <a name="default-behavior"></a>默认行为

`choco-upgrade` 工具的默认行为出错，因为需要 `input` 属性。

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `choco-upgrade` 的示例。

#### <a name="devinitjson-that-will-update-packages-listed-in-packagesconfig"></a>将更新 packages.config 中列出的包的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "choco-upgrade",
            "input": "packages.config",
        }
    ]
}
```

#### <a name="devinitjson-that-will-upgrade-mongodb"></a>将升级 MongoDB 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "choco-upgrade",
            "input": "mongodb"
        }
    ]
}
```

#### <a name="devinitjson-that-will-upgrade-to-a-specific-version-of-mongodb"></a>将升级到特定版本 MongoDB 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "choco-upgrade",
            "input": "mongodb",
            "additionalOptions": "--version 4.2.7"
        }
    ]
}
```