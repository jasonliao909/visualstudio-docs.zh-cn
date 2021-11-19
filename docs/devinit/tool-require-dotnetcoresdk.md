---
title: require-dotnetcoresdk
description: devinit 工具需要-dotnetcoresdk。
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
ms.openlocfilehash: 1963ad8dfe1bd31eb3f98ec6fdf57524a274cfb6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832980"
---
# <a name="require-dotnetcoresdk"></a>require-dotnetcoresdk

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该 `require-dotnetcoresdk` 工具用于通过[dotnet](/dotnet/core/tools/dotnet-install-script)脚本安装[.NET Core SDK](https://dotnet.microsoft.com/)和共享运行时。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性均省略或为空，则该工具将遵循下面详细说明的 [默认](#default-behavior) 行为。

| 名称                                             | 类型   | 必须 | 值                                                                               |
|--------------------------------------------------|--------|----------|-------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                               |
| [**送**](#input)                              | 字符串型 | 否       | 要安装的 .NET Core SDK 的版本。 有关详细信息，请参阅以下 [输入](#input) 。 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息，请参阅下面的 [其他选项](#additional-options) 。                    |

### <a name="input"></a>输入

`input`属性用于指定要安装的 .NET Core SDK 版本。 可在 [dotnet 站点](https://dotnet.microsoft.com/download/dotnet-core)上找到版本列表。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为的值传入 `additionalOptions` 。 这些自变量直接传递到 [dotnet](/dotnet/core/tools/dotnet-install-script) 脚本中使用的自变量。 有关可用参数的详细信息，请参阅[dotnet](/dotnet/core/tools/dotnet-install-script)的[文档](/dotnet/core/tools/dotnet-install-script)。 使用时 `additionalOptions` ，请确保使用 PowerShell 参数名称和格式。

> [!NOTE]
> 包含空格的参数的任何其他值必须包含一对使用反斜杠)  (的转义引号。 示例用法中显示了使用的 [示例](#example-usage) `-InstallDir` 。

### <a name="default-behavior"></a>默认行为

此工具的默认行为 `require-dotnetcoresdk` 是在 `global.json` 当前工作目录中安装 [ (文档) ](/dotnet/core/tools/global-json?tabs=netcore3x) 文件中指定的 .NET Core SDK 版本。 如果未 `global.json` 找到任何文件， `require-dotnetcoresdk` 则将安装最新版本的 .NET Core SDK 和共享运行时。

## <a name="example-usage"></a>用法示例
下面是如何使用运行的示例 `require-dotnetcoresdk` `.devinit.json` 。

#### <a name="devinitjson-that-will-install-the-latest-version-of-net-core"></a>devinit 将安装最新版本的 .NET Core：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetcoresdk"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-net-core"></a>devinit，它将安装特定版本的 .NET Core：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetcoresdk",
            "input": "3.0.0"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-net-core-and-aspnet-core"></a>devinit，它将安装特定版本的 .NET Core 和 ASP.NET Core：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetcoresdk",
            "input": "3.0.0",
            "additionalOptions": "-Runtime aspnetcore"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-net-core-in-a-specific-directory"></a>devinit，它将在特定目录中安装 .NET Core：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetcoresdk",
            "additionalOptions": "-InstallDir \"C:\\Program Files\\dotnet\""
        }
    ]
}
```