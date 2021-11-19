---
title: require-dotnetframeworksdk
description: devinit 工具需要-dotnetframeworksdk。
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
ms.openlocfilehash: 0c40ebfd2a8b665a1421ba70c0f785774e97d3df
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832977"
---
# <a name="require-dotnetframeworksdk"></a>require-dotnetframeworksdk

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该 `require-dotnetframeworksdk` 工具用于通过[提供的安装](https://dotnet.microsoft.com/download/visual-studio-sdks)程序安装[.NET Framework SDK](https://dotnet.microsoft.com/) 。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性均省略或为空，则该工具将遵循下面详细说明的 [默认](#default-behavior) 行为。

| 名称                                             | 类型   | 必须  | 值                                                                                    |
|--------------------------------------------------|--------|-----------|------------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否        | 可选注释属性。 未使用。                                                    |
| [**送**](#input)                              | 字符串型 | 否        | 要安装的 .NET Framework SDK 的版本。 有关详细信息，请参阅以下 [输入](#input) 。 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否        | 未使用。 有关详细信息，请参阅下面的 [其他选项](#additional-options) 。               |

### <a name="input"></a>输入

`input`属性用于指定要安装的 .NET Framework SDK 版本。 可在 [dotnet 站点](https://dotnet.microsoft.com/download/visual-studio-sdks)上找到版本列表。

### <a name="additional-options"></a>附加选项

未使用。

### <a name="default-behavior"></a>默认行为

此工具的默认行为 `require-dotnetframeworksdk` 是安装最新版本。 请参阅 [提供](https://dotnet.microsoft.com/download/visual-studio-sdks) 的适用于最新版本的安装程序。

## <a name="example-usage"></a>用法示例
下面是如何使用运行的示例 `require-dotnetframeworksdk` `.devinit.json` 。

#### <a name="devinitjson-that-will-install-the-latest-net-framework"></a>devinit 将安装最新 .NET Framework：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetframeworksdk"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-the-net-framework"></a>devinit，它将安装 .NET Framework 的特定版本：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetframeworksdk",
            "input": "4.8.0"
        }
    ]
}
```