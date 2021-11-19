---
title: choco-install
description: 用于安装 Chocolatey 包的 devinit tool choco-install。
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
ms.openlocfilehash: c1f5b1c587ea8d1d6335e19b2e7303cc12ad9783
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833001"
---
# <a name="choco-install"></a>choco-install

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`choco-install` 工具可以用来安装和更新 [chocolatey](https://chocolatey.org/) 包。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性被省略或为空，则该工具将不执行任何操作。

| 名称                                             | 类型   | 必须  | 值                                                                                                          |
|--------------------------------------------------|--------|-----------|----------------------------------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否        | 可选注释属性。 未使用。                                                                          |
| [input](#input)                              | 字符串 | 是       | 要安装的程序包。 有关详细信息，请参阅下方的 [Input](#input)。                                                 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否        | 要传递给该工具的其他选项。 有关详细信息，请参阅下方的[其他选项](#additional-options)。       |

### <a name="input"></a>输入

`input` 属性用于指定要安装的包的名称（例如“mongodb”）或以下格式的配置文件路径 packages.config、.nuspec 和 .nupkg。 `input` 值将追加到 `choco install` 命令（例如 `choco install mongodb`），以及 [`additionalOptions`](#additional-options) 中特定的任何参数和内置 `choco` 选项（如[下面](#built-in-options)所定义的）。 包位于 [Chocolatey 包库](https://chocolatey.org/packages)中。 使用配置文件时，可以在 `input` 属性中传递该文件的路径，例如 `"input":"packages.config"`。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为 `additionalOptions` 值传入。 这些参数直接传递到由 [`choco install`](https://chocolatey.org/docs/commands-install) 使用的参数并在 chocolatey 文档中定义。

#### <a name="adding-new-feeds-to-chocolatey"></a>向 Chocolatey 添加新源
如果要向 Chocolatey 添加新源，与 `choco source add` 命令类似，可以传入 `additionalOptions` 来实现此操作。 [示例用法](#example-usage)中演示了如何添加一个新源。 如果希望添加专用源，则建议在命令提示符下运行该工具，因为它需要凭据。 例如 `devinit run -t choco-install -i {package} -s "{feed link}" -u {user} -p {password}`，其中 `{package}`、`{feed link}`、`{user}` 和 `{password}` 引用你的特定包、源链接、用户名和密码。 有关详细信息，请参阅上面的 Chocolatey 文档。 

### <a name="built-in-options"></a>内置选项

`choco-install` 工具设置了多个 `choco` 命令行参数，以确保 `choco` 能够无外设运行。 下面列出了这些参数，相关文档可在 [chocolatey 文档](https://chocolatey.org/docs/)中找到。

| 名称                  | 说明                                                                                        |
|-----------------------|----------------------------------------------------------------------------------------------------|
| **--yes**             | 确认所有提示 - 选择肯定回答而不是提示。 意味着 `--accept-license.`。 |
| --no-progress     | 不显示进度 - 不显示进度百分比。                                         |
| --skip-powershell | 跳过 PowerShell - chocolateyInstall.ps1 不会运行。                                              |

### <a name="default-behavior"></a>默认行为

`choco-install` 工具的默认行为出错，因为需要 `input` 属性。

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `choco-install` 的示例。

#### <a name="devinitjson-that-will-install-packages-listed-in-packagesconfig"></a>将安装 packages.config 中列出的包的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "choco-install",
            "input": "packages.config",
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-mongodb"></a>将安装 MongoDB 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "choco-install",
            "input": "mongodb"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-mongodb"></a>将安装特定版本 MongoDB 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "choco-install",
            "input": "mongodb",
            "additionalOptions": "--version 4.2.7"
        }
    ]
}
```

#### <a name="devinitjson-that-adds-a-new-feed-to-chocolatey"></a>将新源添加到 Chocolatey 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "choco-install",
            "input": "packages.config",
            "additionalOptions": "-s '{feed link}'"
        }
    ]
}
```