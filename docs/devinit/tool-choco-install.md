---
title: choco-install
description: 用于安装 Chocolatey 包的 devinit 工具 choco。
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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该 `choco-install` 工具可用于安装和更新 [chocolatey](https://chocolatey.org/) 包。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性均省略或为空，则该工具将不执行任何操作。

| 名称                                             | 类型   | 必须  | 值                                                                                                          |
|--------------------------------------------------|--------|-----------|----------------------------------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否        | 可选注释属性。 未使用。                                                                          |
| [**送**](#input)                              | 字符串 | 是       | 要安装的程序包。 有关详细信息，请参阅以下 [输入](#input) 。                                                 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否        | 要传递给该工具的其他选项。 有关详细信息，请参阅下面的 [其他选项](#additional-options) 。       |

### <a name="input"></a>输入

`input`属性用于指定要安装的包的名称 (例如 "mongodb" ) 或以下格式的配置文件的路径 _packages.config_ _nuspec_ 和 _. nupkg_。 的值 `input` 将追加到 `choco install` 命令 (例如 `choco install mongodb`) ，以及中特定的任何参数 [`additionalOptions`](#additional-options) 以及在 `choco` [下面](#built-in-options)) 定义 (的内置选项。 包位于 [Chocolatey 包库](https://chocolatey.org/packages)中。 当使用配置文件时，可以在属性中传入该文件的路径 `input` ，例如 `"input":"packages.config"` 。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为的值传入 `additionalOptions` 。 这些自变量直接传递到由使用的自变量， [`choco install`](https://chocolatey.org/docs/commands-install) 并在 chocolatey 文档中定义。

#### <a name="adding-new-feeds-to-chocolatey"></a>向 Chocolatey 添加新源
如果要向 Chocolatey 添加新的源（与命令类似）， `choco source add` 可以传入 `additionalOptions` 。 [示例用法](#example-usage)中添加了一个新的源。 如果希望添加专用源，则建议在命令提示符下运行该工具，因为它需要凭据。 例如，， `devinit run -t choco-install -i {package} -s "{feed link}" -u {user} -p {password}` 其中 `{package}` ，、 `{feed link}` 、 `{user}` 和 `{password}` 引用你的特定包、源链接、用户名和密码。 有关详细信息，请参阅上面的 Chocolatey 文档。 

### <a name="built-in-options"></a>内置选项

该 `choco-install` 工具设置了多个 `choco` 命令行参数，以确保 `choco` 能够运行无外设。 下面列出了这些自变量，这些自变量可在 [chocolatey 文档](https://chocolatey.org/docs/)中找到。

| 名称                  | 说明                                                                                        |
|-----------------------|----------------------------------------------------------------------------------------------------|
| **--yes**             | 确认所有提示-选择赞成答案而不是提示。 涉及 `--accept-license.` |
| **--无进度**     | 不显示进度-不显示进度百分比。                                         |
| **--skip-powershell** | 跳过 PowerShell-chocolateyInstall.ps1 不会运行。                                              |

### <a name="default-behavior"></a>默认行为

此工具的默认行为 `choco-install` 是 "错误"，因为 `input` 属性是必需的。

## <a name="example-usage"></a>用法示例
下面是如何使用运行的示例 `choco-install` `.devinit.json` 。

#### <a name="devinitjson-that-will-install-packages-listed-in-packagesconfig"></a>devinit，它将安装 packages.config 中列出的包：
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

#### <a name="devinitjson-that-will-install-mongodb"></a>devinit 将安装 MongoDB：
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

#### <a name="devinitjson-that-will-install-a-specific-version-of-mongodb"></a>devinit，它将安装特定版本的 MongoDB：
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

#### <a name="devinitjson-that-adds-a-new-feed-to-chocolatey"></a>devinit，用于将新的源添加到 Chocolatey：
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