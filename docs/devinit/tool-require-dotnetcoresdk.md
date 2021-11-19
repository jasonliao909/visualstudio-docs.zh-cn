---
title: require-dotnetcoresdk
description: devinit 工具 require-dotnetcoresdk。
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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`require-dotnetcoresdk` 工具用于通过 [dotnet-install](/dotnet/core/tools/dotnet-install-script) 脚本安装 [.NET Core SDK](https://dotnet.microsoft.com/) 和共享运行时。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性被省略或为空，则该工具将遵循下面详述的[默认](#default-behavior)行为。

| 名称                                             | 类型   | 必须 | 值                                                                               |
|--------------------------------------------------|--------|----------|-------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                               |
| [input](#input)                              | 字符串型 | 否       | 要安装的 .NET Core SDK 版本。 有关详细信息，请参阅下方的 [Input](#input)。 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息，请参阅下方的[其他选项](#additional-options)。                    |

### <a name="input"></a>输入

`input` 属性用于指定要安装的 .NET Core SDK 版本。 可在 [dotnet-core 站点](https://dotnet.microsoft.com/download/dotnet-core)上找到版本列表。

### <a name="additional-options"></a>附加选项

可以将其他配置选项作为 `additionalOptions` 的值传入。 这些参数直接传递到由 [dotnet-install](/dotnet/core/tools/dotnet-install-script) 脚本使用的参数。 有关可用参数的详细信息，请参阅适用于 [dotnet-install](/dotnet/core/tools/dotnet-install-script) 脚本的[文档](/dotnet/core/tools/dotnet-install-script)。 在使用 `additionalOptions` 时，请确保使用 PowerShell 参数名称和格式。

> [!NOTE]
> 包含空格的参数的任何其他值必须再包含一对转义引号（使用反斜杠）。 [示例用法](#example-usage)中提供了一个使用 `-InstallDir` 的示例。

### <a name="default-behavior"></a>默认行为

`require-dotnetcoresdk` 工具的默认行为是在当前工作目录中安装 `global.json`[（文档）](/dotnet/core/tools/global-json?tabs=netcore3x)文件中指定的 .NET Core SDK 版本。 如果未找到任何 `global.json` 文件，`require-dotnetcoresdk` 将安装最新版本的 .NET Core SDK 和共享运行时。

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `require-dotnetcoresdk` 的示例。

#### <a name="devinitjson-that-will-install-the-latest-version-of-net-core"></a>将安装最新版本 .NET Core 的 .devinit.json：
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

#### <a name="devinitjson-that-will-install-a-specific-version-of-net-core"></a>将安装特定版本 .NET Core 的 .devinit.json：
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

#### <a name="devinitjson-that-will-install-a-specific-version-of-net-core-and-aspnet-core"></a>将安装特定版本 .NET Core 和 ASP.NET Core 的 .devinit.json：
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

#### <a name="devinitjson-that-will-install-net-core-in-a-specific-directory"></a>将在特定目录中安装 .NET Core 的 .devinit.json：
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