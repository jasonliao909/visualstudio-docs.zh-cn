---
title: vcpkg-install
description: devinit tool vcpkg-install。
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
ms.openlocfilehash: 8a4cbe6bd1da12985da87d2f872dc74f988ef213
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832976"
---
# <a name="vcpkg-install"></a>vcpkg-install

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`vcpkg-install` 工具用于使用 [vcpkg](https://github.com/microsoft/vcpkg) 获取 C/C++ 库（称为端口）。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性被省略或为空，则该工具将遵循下面详述的[默认](#default-behavior)行为。

| 名称                                             | 类型   | 必须 | 值                                                                                   |
|--------------------------------------------------|--------|----------|-----------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                                   |
| [input](#input)                              | 字符串 | 是      | 要安装的包。 有关详细信息，请参阅下方的 [Input](#input)。                       |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息，请参阅下方的[其他选项](#additional-options)。                        |

### <a name="input"></a>输入

`input` 属性应为要安装的 `vcpkg` 的 `name`，或者是用于安装多个包的以空格分隔的名称列表。 可在 [vcpkg GitHub 存储库](https://github.com/microsoft/vcpkg/tree/master/ports)中找到可用端口列表。

### <a name="additional-options"></a>附加选项

其他选项将直接传递到 [vcpkg](/powershell/module/powershellget/install-module?view=powershell-7&preserve-view=true) 命令，并记录在 [vcpkg GitHub 存储库](https://github.com/microsoft/vcpkg/blob/master/docs/examples/installing-and-using-packages.md)中。

### <a name="default-behavior"></a>默认行为

`vcpkg-install` 工具的默认行为出错，因为需要 `input`。

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `vcpkg-install` 的示例。

#### <a name="devinitjson-that-will-install-the-sdl2-port"></a>将安装 sdl2 端口的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "vcpkg-install",
            "input": "sdl2",
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-multiple-ports"></a>将安装多个端口的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [

        {
            "tool": "vcpkg-install",
            "input": "sdl2 sqlite3"
        }
    ]
}
```