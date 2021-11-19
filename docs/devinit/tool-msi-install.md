---
title: msi-install
description: 用于 msiexec 的 devinit 工具。
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
ms.openlocfilehash: d2da7f26501cfa686cd0703f7dbbbef4053f761b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832995"
---
# <a name="msi-install"></a>msi-install

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`msi-install` 工具用于使用 [msiexec](https://docs.microsoft.com/windows-server/administration/windows-commands/msiexec) 安装 `.msi` 包装文件格式。

## <a name="usage"></a>使用情况

如果 `input` 省略或为空，则该工具将输出错误。

| 名称                                         | 类型   | 必须 | 值                                                                             |
|----------------------------------------------|--------|----------|-----------------------------------------------------------------------------------|
| **注释**                                 | 字符串型 | 否       | 可选注释属性。 未使用。                                             |
| [input](#input)                          | 字符串 | 是      | 要安装的 `msi`。 有关详细信息，请参阅下方的 [Input](#input)。                      |
| [**additionalOptions**](#additional-options) | 字符串型 | 否       | 有关详细信息，请参阅下方的[其他选项](#additional-options)。                  |

### <a name="input"></a>输入

输入属性用于指定将安装到 `.msi` 文件的路径或 URL。 如果到 `.msi` 的路径不正确，或者 URL 未直接指向 `.msi`，则 `msi-install` 将注意到无法打开安装程序包。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为 additionalOptions 的值传入。 这些参数直接传递到由 `msiexec` 使用的参数并在 `msiexec` [文档](https://docs.microsoft.com/windows-server/administration/windows-commands/msiexec)中定义。

### <a name="built-in-options"></a>内置选项

msi-install 工具设置了多个 `msiexec` 命令行参数，以确保 msi 能够无外设运行。 下面列出了这些参数，相关文档可在 `msiexec` [文档](https://docs.microsoft.com/windows-server/administration/windows-commands/msiexec)中找到。

| 名称          | 说明                                                                                                                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /i            | 运行正常安装                                                                                                                                                                    |
| /quiet        | 指定安静模式，无需用户交互                                                                                                                                        |
| /qn           | 指定在安装过程中没有 UI                                                                                                                                           |
| /passive      | 指定安装仅显示进度栏的无人参与模式                                                                                                                    |
| /l*V          | 启用日志记录，并将所有信息（包括详细信息）记录到计算机的本地临时文件夹中的 `devinit.log` 文件。 如果该工具失败，将显示日志文件路径。      |
| /norestart    | 安装完成后停止计算机重新启动，但如果需要重新启动，则将返回3010 退出代码                                                                  |

### <a name="default-behavior"></a>默认行为

`msi-install` 工具的默认行为出错，因为需要 `input` 属性。

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `msi-install` 的示例。

#### <a name="devinitjson-that-will-install-the-7-zip-msi"></a>.devinit.json 将安装 7-Zip MSI：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-4.0",
    "run": [
        {
            "tool": "msi-install",
            "input": "https://www.7-zip.org/a/7z1900.msi"
        }
    ]
}
```
