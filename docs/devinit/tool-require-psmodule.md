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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。


`require-psmodule` 工具用于通过 [Install-Module](/powershell/module/powershellget/install-module?view=powershell-7&preserve-view=true) 从 [PowerShell 库](https://www.powershellgallery.com/)安装一个 [PowerShell 模块](/powershell/scripting/developer/module/understanding-a-windows-powershell-module?view=powershell-7&preserve-view=true)，以便在 PowerShell 脚本中使用它。

> [!TIP]
> 安装模块后，仍然需要使用 [Import-Module](/powershell/module/microsoft.powershell.core/import-module?view=powershell-7&preserve-view=true) 将它导入到脚本中。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性被省略或为空，则该工具将遵循下面详述的[默认](#default-behavior)行为。

| 名称                                             | 类型   | 必须 | 值                                                                                   |
|--------------------------------------------------|--------|----------|-----------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                                   |
| [input](#input)                              | 字符串 | 是      | 要安装的包。 有关详细信息，请参阅下方的 [Input](#input)。                       |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 未使用。 有关详细信息，请参阅下方的[其他选项](#additional-options)。              |

### <a name="input"></a>输入

`input` 属性应该是要安装的 PowerShell 模块的 `Name`。 可用的 PowerShell 模块的列表可以通过搜索 [PowerShell 库](https://www.powershellgallery.com/)找到。

### <a name="additional-options"></a>附加选项

其他选项将直接传递到 [Install-Module](/powershell/module/powershellget/install-module?preserve-view=true&view=powershell-7) 命令，并记录在 [Microsoft Docs](/powershell/module/powershellget/install-module?preserve-view=true&view=powershell-7) 中。

### <a name="default-behavior"></a>默认行为

该 `require-psmodule` 工具的默认行为出错，因为需要 `input`。

### <a name="built-in-options"></a>内置选项

`require-psmodule` 工具设置了多个 `Install-Module` 命令行参数，以确保 `Install-Module` 能够无外设运行。 下面列出了这些参数，相关文档可在 [Install-Module](/powershell/module/powershellget/install-module?view=powershell-7&preserve-view=true) 中找到。

| 名称         | 说明                                                                                                                                                                                                                                                                                                                                                               |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **-Force**   | 安装一个模块并覆盖有关模块安装冲突的警告消息。 如果计算机上已存在同名的模块，则 Force 允许安装多个版本。 如果存在名称和版本相同的现有模块，将覆盖该模块。 Force 和 AllowClobber 可以在 Install-Module 命令中一起使用。 |
| **-WhatIf**  | -WhatIf 标记是在为 `devinit` 命令传递试运行时添加的。                                                                                                                                                                                                                                                                                                       |
| **-Verbose** | -Verbose 标记是在为 `devinit` 命令传递详细信息时添加的。                                                                                                                                                                                                                                                                                                      |


## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `require-psmodule` 的示例。

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

#### <a name="devinitjson-that-will-install-the-powershellget-module-from-a-specific-repository"></a>将从特定存储库安装 PowerShellGet 模块的 .devinit.json：
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