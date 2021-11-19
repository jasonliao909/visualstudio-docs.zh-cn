---
title: require-azureartifactscredentialprovider
description: devinit 工具需要-azureartifactscredentialprovider。
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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

该 `require-azureartifactscredentialprovider` 工具安装 Azure Artifacts 凭据提供程序。 Azure Artifacts 凭据提供程序可在 .net 开发工作流中自动获取将 NuGet 包还原所需的凭据。 有关详细信息，请参阅[此处](https://github.com/microsoft/artifacts-credprovider/blob/master/README.md)Azure Artifacts 凭据提供程序。

## <a name="usage"></a>使用情况

如果 `input` 和 `additionalOptions` 属性均省略或为空，则该工具将遵循下面详细说明的 [默认](#default-behavior) 行为。

| 名称                                             | 类型   | 必须 | 值                                                                                |
|--------------------------------------------------|--------|----------|--------------------------------------------------------------------------------------|
| **注释**                                     | 字符串型 | 否       | 可选注释属性。 未使用。                                                |
| [**送**](#input)                              | 字符串型 | 否       | 未使用。 有关详细信息，请参阅以下 [输入](#input) 。 |
| [**additionalOptions**](#additional-options)     | 字符串型 | 否       | 有关详细信息，请参阅下面的 [其他选项](#additional-options) 。                     |

### <a name="input"></a>输入

未使用。 如果提到，将忽略任何输入。

### <a name="additional-options"></a>附加选项

其他选项将按原样传递到凭据提供程序命令。

### <a name="default-behavior"></a>默认行为

此工具的默认行为 `require-azureartifactscredentialprovider` 是安装最新版本的 Azure Artifacts 凭据提供程序。

## <a name="example-usage"></a>用法示例
下面是如何使用运行的示例 `require-azureartifactscredentialprovider` `.devinit.json` 。

#### <a name="devinitjson-that-will-install-azure-artifacts-credential-provider"></a>devinit 将安装 Azure Artifacts 凭据提供程序：
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
