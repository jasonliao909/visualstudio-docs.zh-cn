---
title: 从 FxCop 分析器迁移到 .NET 分析器
ms.custom: SEO-VS-2020
description: 了解如何从 FxCop 分析器迁移到 .NET 分析器
ms.date: 03/06/2020
ms.topic: conceptual
f1_keywords:
- vs.projectpropertypages.codeanalysis
helpviewer_keywords:
- FxCop, migration
- legacy analysis, migration
- source code analysis, migration
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: d6f9c36b1b64abe648c3aa9014c633e4e4949b1a
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798253"
---
# <a name="migrate-from-fxcop-analyzers-to-net-analyzers"></a>从 FxCop 分析器迁移到 .NET 分析器

"Roslyn".NET Compiler Platform (分析器) 替换 [托管代码的旧](code-analysis-for-managed-code-overview.md) 分析。 FxCop (中的许多) 已重写为源分析器。

在 2019 Visual Studio 16.8 和 .NET 5.0 之前，这些分析器作为 `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)包 提供。

从 Visual Studio 2019 16.8 和 .NET 5.0 开始，这些分析器 [包含在 .NET SDK 中](/dotnet/fundamentals/code-analysis/overview)。 如果不想移动到 .NET 5+ SDK，或者想要使用基于 NuGet 包的模型，则分析器也可在 NuGet 包 `Microsoft.CodeAnalysis.NetAnalyzers` [中使用](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)。 对于按需版本更新，你可能更倾向于使用基于包的模型。

> [!NOTE]
> 第一方 .NET 分析器与目标平台无关。 也就是说，项目不需要面向特定的 .NET 平台。 分析器适用于面向 以及早期 .NET 版本（如 `net5.0` 、 和 ） `netcoreapp` `netstandard` 的项目 `net472` 。

## <a name="migration-steps"></a>迁移步骤

从版本 `3.3.2` 开始 `Microsoft.CodeAnalysis.FxCopAnalyzers` ，NuGet 包已弃用。 请按照以下步骤将项目或解决方案从 `Microsoft.CodeAnalysis.FxCopAnalyzers` 迁移到 .NET 分析器：

1. 卸载 `Microsoft.CodeAnalysis.FxCopAnalyzers` NuGet 包

2. [启用或安装 .NET 分析器](install-net-analyzers.md)。 请注意，无需更改项目的目标平台。

3. 启用其他规则： `Microsoft.CodeAnalysis.NetAnalyzers` 比 更保守 `Microsoft.CodeAnalysis.FxCopAnalyzers` 。 与 FxCopAnalyzers 包不同，它只有几个正确性规则，这些规则默认作为生成警告 [启用](/dotnet/fundamentals/code-analysis/overview#enabled-rules)。 可以通过 [自定义](/dotnet/fundamentals/code-analysis/overview#enable-additional-rules) [AnalysisMode](/dotnet/core/project-sdk/msbuild-props#analysismode) MSBuild 属性来启用其他规则。 例如，将 属性设置为 `AllEnabledByDefault` 将默认启用所有适用的 CA 规则作为生成警告。

   ```xml
   <PropertyGroup>
     <AnalysisMode>AllEnabledByDefault</AnalysisMode>
   </PropertyGroup>
   ```

## <a name="see-also"></a>请参阅

- [源代码分析与传统分析](net-analyzers-faq.yml#what-s-the-difference-between-legacy-fxcop-and--net-analyzers-)
- [从旧版分析迁移到 .NET 分析器](migrate-from-legacy-analysis-to-net-analyzers.md)
- [启用或安装 .NET 分析器](install-net-analyzers.md)
- [有关 .NET 分析器常见问题解答](net-analyzers-faq.yml)
- [配置 .NET 分析器](/dotnet/fundamentals/code-analysis/code-quality-rule-options)
