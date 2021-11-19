---
title: enable-iis
description: devinit 工具 enable-iis。
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
ms.openlocfilehash: eecdc2a020117b7345682068cb27509df805ff9b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832999"
---
# <a name="enable-iis"></a>enable-iis

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`enable-iis` 工具用于启用 IIS 功能并安装 [ASP.NET Core 模块](/aspnet/core/host-and-deploy/aspnet-core-module)，以便使用 IIS 进行 ASP.NET 开发。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性省略或为空，则该工具将遵循下面详述的[默认](#default-behavior)行为。

| 名称                                             | 类型   | 必须 | 值                                                                               |
|--------------------------------------------------|--------|----------|-------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                               |
| [input](#input)                              | 字符串型 | 否       | 未使用。                                                                           |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 未使用。                                                                           |

### <a name="input"></a>输入

未使用。

### <a name="additional-options"></a>附加选项

未使用。

### <a name="default-behavior"></a>默认行为

`enable-iis` 工具的默认行为是启用 IIS 功能：IIS-WebServer、IIS-WebServerRole、IIS-WebSockets 和 IIS-WebAuthentication，然后安装包含 ASP.NET Core 模块的最新版本的 ASP.NET 托管捆绑包。

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `enable-iis` 的示例。

#### <a name="devinitjson-that-will-enable-iis-development"></a>将启用 IIS 开发的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0.json",
    "run": [
        {
            "tool": "enable-iis"
        },
    ]
}
```