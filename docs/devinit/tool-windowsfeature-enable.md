---
title: windowsfeature-enable
description: devinit 工具 windowsfeature-enable。
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
ms.openlocfilehash: ea3716cfd244cb81d6c380d2787babf5845c490a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833101"
---
# <a name="windowsfeature-enable"></a>windowsfeature-enable

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们专注于为云支持的内部循环和 VDI 解决方案提供不断发展的体验，这些解决方案针对一组广泛的Visual Studio工作负载进行优化。 作为此和 `devinit` 关联工具的一部分，将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`windowsfeature-enable`该工具用于启用Windows功能。

## <a name="usage"></a>使用情况

| 名称                                             | 类型   | 必须 | 值                                                                    |
|--------------------------------------------------|--------|----------|--------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                    |
| [**输入**](#input)                              | 字符串 | 是      | 要Windows的 Windows 功能。 有关详细信息 [，](#input) 请参阅下面的输入。   |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息 [，请参阅](#additional-options) 下面的其他选项。         |

### <a name="input"></a>输入

`input`属性应为要安装的 `name` 的 `windows feature` 。 可以通过运行 PowerShell cmd 找到可用 `Get-WindowsFeature` 功能的列表。

### <a name="additional-options"></a>Additional-Options

无。

### <a name="default-behavior"></a>默认行为

该工具的默认 `windowsfeature-enable` 行为是按要求 `input` 出错。

## <a name="example-usage"></a>用法示例
下面是如何使用 运行 `windowsfeature-enable` 的示例 `.devinit.json` 。

#### <a name="devinitjson-that-will-install-iis"></a>将安装 IIS 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "windowsfeature-enable",
            "input": "web-server",
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-the-net-framework"></a>.devinit.json，它将安装.NET Framework：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "windowsfeature-enable",
            "input": "net-framework-features"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-the-net-framework-45"></a>将安装 .NET Framework 4.5 的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "windowsfeature-enable",
            "input": "net-framework-45-features"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-the-windows-subsystem-for-linux-20"></a>.devinit.json，它将安装 适用于 Linux 的 Windows 子系统 2.0：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "windowsfeature-enable",
            "input": "Microsoft-Windows-Subsystem-Linux"
        }
    ]
}
```
