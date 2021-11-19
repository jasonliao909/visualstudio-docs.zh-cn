---
title: choco-upgrade
description: devinit 工具 choco-upgrade。
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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们专注于为云支持的内部循环和 VDI 解决方案提供不断发展的体验，这些解决方案针对一组广泛的Visual Studio工作负载进行优化。 作为此和 `devinit` 关联工具的一部分，将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`choco-upgrade`该工具可用于安装和更新[巧克力包](https://chocolatey.org/docs/commandsupgrade)。

## <a name="usage"></a>使用情况

如果省略 `input` 和 `additionalOptions` 属性或属性为空，则该工具不执行任何操作。

| 名称                                             | 类型   | 必须  | 值                                                                                                          |
|--------------------------------------------------|--------|-----------|----------------------------------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否        | 可选注释属性。 未使用。                                                                          |
| [**输入**](#input)                              | 字符串 | 是       | 要升级的包。 有关详细信息 [，](#input) 请参阅下面的输入。                                                 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否        | 要传递给工具的其他选项。 有关详细信息 [，请参阅](#additional-options) 下面的其他选项。       |

### <a name="input"></a>输入

属性用于指定要升级 (的包的名称，例如"mongodb") 或以下格式的配置文件的路径 `input` _packages.config、.nuspec_ 和 _.nupkg_。 的值将追加到命令参数中 (例如) 以及 中特定的任何参数，以及下面定义的 (`input` `choco upgrade` `choco upgrade mongodb` [`additionalOptions`](#additional-options) `choco` [选项](#built-in-options)) 。 可以在 Chocolatey 包 [库中找到包](https://chocolatey.org/packages)。 使用配置文件时，可以在 属性中传递该文件的路径 `input` ，例如 `"input":"packages.config"` ：。

### <a name="additional-options"></a>附加选项

其他配置选项可以作为 的值传入 `additionalOptions` 。 这些参数是直接传递给 使用的参数， [`choco upgrade`](https://chocolatey.org/docs/commands-upgrade) 在 chocolatey 文档中定义。

### <a name="built-in-options"></a>内置选项

`choco-upgrade`该工具设置许多 `choco` 命令行参数，以确保 `choco` 可以无头运行。 下面列出了这些参数，有关这些参数的文档可在 [chocolatey 文档 找到](https://chocolatey.org/docs/)。

| 名称                  | 说明                                                                                        |
|-----------------------|----------------------------------------------------------------------------------------------------|
| **--yes**             | 确认所有提示 - 选择答案而不是提示。 意味着 `--accept-license`。 |
| **--no-progress**     | 不显示进度 - 不会显示进度百分比。                                         |
| **--skip-powershell** | 跳过 PowerShell - chocolateyInstall.ps1不会运行。                                              |

### <a name="default-behavior"></a>默认行为

该工具的默认行为 `choco-upgrade` 是出错，因为 `input` 属性是必需的。

## <a name="example-usage"></a>用法示例
下面是如何使用 运行 `choco-upgrade` 的示例 `.devinit.json` 。

#### <a name="devinitjson-that-will-update-packages-listed-in-packagesconfig"></a>将更新以下项中列出的包的 .devinit.json packages.config：
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

#### <a name="devinitjson-that-will-upgrade-to-a-specific-version-of-mongodb"></a>将升级到特定版本的 MongoDB 的 .devinit.json：
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