---
title: require-azureartifactscredentialprovider
description: devinit 工具 require-azureartifactscredentialprovider。
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
ms.openlocfilehash: e5ba9847b09f06f853f48a0885de5e0d63664fac
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832983"
---
# <a name="require-azureartifactscredentialprovider"></a>require-azureartifactscredentialprovider

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`require-azureartifactscredentialprovider` 工具安装 Azure Artifacts 凭据提供程序。 Azure Artifacts 凭据提供程序可在 .NET 开发工作流中自动获取还原 NuGet 包所需的凭据。 有关 Azure Artifacts 凭据提供程序的详细信息，请参阅[此处](https://github.com/microsoft/artifacts-credprovider/blob/master/README.md)。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性被省略或为空，则该工具将遵循下面详述的[默认](#default-behavior)行为。

| 名称                                             | 类型   | 必须 | 值                                                                                |
|--------------------------------------------------|--------|----------|--------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                                |
| [input](#input)                              | 字符串型 | 否       | 未使用。 有关详细信息，请参阅下方的 [input](#input)。 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息，请参阅下方的[其他选项](#additional-options)。                     |

### <a name="input"></a>输入

未使用。 如果提到，请忽略任何输入。

### <a name="additional-options"></a>附加选项

附加选项按原样传递到凭据提供程序命令。

### <a name="default-behavior"></a>默认行为

`require-azureartifactscredentialprovider` 工具的默认行为是安装最新版本的 Azure Artifacts 凭据提供程序。

## <a name="example-usage"></a>用法示例
下面是有关如何使用 `.devinit.json` 运行 `require-azureartifactscredentialprovider` 的示例。

#### <a name="devinitjson-that-will-install-azure-artifacts-credential-provider"></a>将安装 Azure Artifacts 凭据提供程序的 .devinit.json：
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-azureartifactscredentialprovider",
        }
    ]
}
```
