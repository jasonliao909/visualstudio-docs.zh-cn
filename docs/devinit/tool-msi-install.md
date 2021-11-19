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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该 `msi-install` 工具用于 `.msi` 使用 [msiexec](https://docs.microsoft.com/windows-server/administration/windows-commands/msiexec)安装包文件格式。

## <a name="usage"></a>使用情况

如果 `input` 省略或为空，则该工具将输出错误。

| 名称                                         | 类型   | 必须 | 值                                                                             |
|----------------------------------------------|--------|----------|-----------------------------------------------------------------------------------|
| **注释**                                 | 字符串型 | 否       | 可选注释属性。 未使用。                                             |
| [**送**](#input)                          | 字符串 | 是      | 要安装的 `msi`。 有关详细信息，请参阅以下 [输入](#input) 。                      |
| [**additionalOptions**](#additional-options) | 字符串型 | 否       | 有关详细信息，请参阅下面的 [其他选项](#additional-options) 。                  |

### <a name="input"></a>输入

输入属性用于指定 `.msi` 将安装的文件的路径或 URL。 如果到的路径不 `.msi` 正确，或者 URL 未 `.msi` 直接指向，则 `msi-install` 会注意到无法打开安装程序包。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为其他的值传入。 这些自变量直接传递到由使用的自变量 `msiexec` ，并在 `msiexec` [文档](https://docs.microsoft.com/windows-server/administration/windows-commands/msiexec)中定义。

### <a name="built-in-options"></a>内置选项

Msi 安装工具会设置多个 `msiexec` 命令行参数，以确保 msi 可以运行无外设。 下面列出了这些参数，并在文档中找到了这些参数的相关文档 `msiexec` [](https://docs.microsoft.com/windows-server/administration/windows-commands/msiexec)。

| 名称          | 说明                                                                                                                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /i            | 运行正常安装                                                                                                                                                                    |
| /quiet        | 指定静默模式，无需用户交互                                                                                                                                        |
| /qn           | 指定在安装过程中没有 UI                                                                                                                                           |
| /passive      | 指定安装仅显示进度栏的无人参与模式                                                                                                                    |
| /l * V          | 启用日志记录，并将所有信息（包括详细信息）记录到 `devinit.log` 计算机的本地临时文件夹中的文件。 如果该工具失败，将显示日志文件路径。      |
| /norestart    | 安装完成后停止计算机重新启动，但如果需要重新启动，则将返回3010退出代码                                                                  |

### <a name="default-behavior"></a>默认行为

此工具的默认行为 `msi-install` 是 "错误"，因为 `input` 属性是必需的。

## <a name="example-usage"></a>用法示例
下面是如何使用运行的示例 `msi-install` `.devinit.json` 。

#### <a name="devinitjson-that-will-install-the-7-zip-msi"></a>devinit，它将安装 7-Zip MSI：
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
