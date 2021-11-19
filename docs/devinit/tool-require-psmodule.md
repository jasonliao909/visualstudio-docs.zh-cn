---
title: require-psmodule
description: devinit 工具 require-psmodule。
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
ms.openlocfilehash: cdb37bf4e714cfc25e5bf82354856fd4d3d63e87
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833110"
---
# <a name="require-psmodule"></a>require-psmodule

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们专注于为云支持的内部循环和 VDI 解决方案提供不断发展的体验，这些解决方案针对一组广泛的Visual Studio工作负载进行优化。 作为此和 `devinit` 关联工具的一部分，将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。


`require-psmodule`该工具用于通过[Install-Module](/powershell/module/powershellget/install-module?view=powershell-7&preserve-view=true)从 PowerShell 库安装[](https://www.powershellgallery.com/) [PowerShell](/powershell/scripting/developer/module/understanding-a-windows-powershell-module?view=powershell-7&preserve-view=true)模块，以便可以在 PowerShell 脚本中使用。

> [!TIP]
> 安装模块后，仍然需要使用 [Import-Module 将其导入到脚本中](/powershell/module/microsoft.powershell.core/import-module?view=powershell-7&preserve-view=true)。

## <a name="usage"></a>使用情况

如果省略 `input` 和 属性或属性 `additionalOptions` 为空，该工具将遵循 [下面详述](#default-behavior) 的默认行为。

| 名称                                             | 类型   | 必须 | 值                                                                                   |
|--------------------------------------------------|--------|----------|-----------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                                   |
| [**输入**](#input)                              | 字符串 | 是      | 包 () 安装。 有关详细信息 [，](#input) 请参阅下面的输入。                       |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 未使用。 有关详细信息 [，请参阅](#additional-options) 下面的其他选项。              |

### <a name="input"></a>输入

`input`属性应为要安装的 `Name` PowerShell 模块的 。 可以通过在 中搜索找到可用 PowerShell 模块[PowerShell 库。](https://www.powershellgallery.com/)

### <a name="additional-options"></a>附加选项

其他选项直接传递给[Install-Module](/powershell/module/powershellget/install-module?preserve-view=true&view=powershell-7)命令，并记录在[Microsoft Docs。](/powershell/module/powershellget/install-module?preserve-view=true&view=powershell-7)

### <a name="default-behavior"></a>默认行为

该工具的默认 `require-psmodule` 行为是按要求 `input` 出错。

### <a name="built-in-options"></a>内置选项

`require-psmodule`该工具设置许多 `Install-Module` 命令行参数，以确保 `Install-Module` 可以无头运行。 下面列出了这些参数，有关这些参数的文档可在 [Install-Module 中找到](/powershell/module/powershellget/install-module?view=powershell-7&preserve-view=true)。

| 名称         | 说明                                                                                                                                                                                                                                                                                                                                                               |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **-Force**   | 安装模块并替代有关模块安装冲突的警告消息。 如果计算机上已存在同名的模块，则 Force 允许安装多个版本。 如果存在名称和版本相同的现有模块，将覆盖模块。 Force 和 AllowClobber 可以在命令中一Install-Module使用。 |
| **-WhatIf**  | -为 命令传递干运行时，将添加 WhatIf `devinit` 标志。                                                                                                                                                                                                                                                                                                       |
| **-Verbose** | 为 命令传递 verbose 时，将添加 -Verbose `devinit` 标志。                                                                                                                                                                                                                                                                                                      |


## <a name="example-usage"></a>用法示例
下面是如何使用 运行 `require-psmodule` 的示例 `.devinit.json` 。

#### <a name="devinitjson-that-will-install-the-powershellget-module"></a>将安装 PowerShellGet 模块的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-psmodule",
            "input": "PowerShellGet",
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-the-powershellget-module-from-a-specific-repository"></a>.devinit.json，它将从特定存储库安装 PowerShellGet 模块：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-psmodule",
            "input": "PowerShellGet",
            "additionalOptions": "-Repository PSGallery"
        }
    ]
}
```