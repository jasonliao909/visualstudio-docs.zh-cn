---
title: 从 FxCop 分析器迁移到 .NET 分析器
ms.custom: SEO-VS-2020
description: 了解如何从 FxCop 分析器迁移到 .NET 分析器。
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
ms.technology: vs-ide-code-analysis
ms.openlocfilehash: 479c5cfdffa8c25960f2172592de37731dc6e5b2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601275"
---
# <a name="migrate-from-fxcop-analyzers-to-net-analyzers"></a>从 FxCop 分析器迁移到 .NET 分析器

.NET Compiler Platform（“Roslyn”）分析器的源代码分析取代了托管代码的[传统分析](code-analysis-for-managed-code-overview.md)。 许多传统分析 (FxCop) 规则已被重新编写为源分析器。

在低于 Visual Studio 2019 16.8 和 .NET 5.0 的版本中，这些分析器作为 `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)提供。

从 Visual Studio 2019 16.8 和 .NET 5.0 开始，这些分析器[包含在 .NET SDK 中](/dotnet/fundamentals/code-analysis/overview)。 如果不想迁移到 .NET 5+ SDK，或者更喜欢基于 NuGet 包的模型，则 `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)中也提供了这些分析器。 对于按需版本更新，你可能更倾向于使用基于包的模型。

> [!NOTE]
> 第一方 .NET 分析器与目标平台无关。 即，项目不需要面向特定的 .NET 平台。 分析器适用于面向 `net5.0` 及早期 .NET 版本（如 `netcoreapp`、`netstandard` 和 `net472`）的项目。

## <a name="migration-steps"></a>迁移步骤

从版本 `3.3.2` 开始，不建议使用 `Microsoft.CodeAnalysis.FxCopAnalyzers` NuGet 包。 请按照以下步骤将项目或解决方案从 `Microsoft.CodeAnalysis.FxCopAnalyzers` 迁移到 .NET 分析器：

1. 卸载 `Microsoft.CodeAnalysis.FxCopAnalyzers` NuGet 包

2. [启用或安装 .NET 分析器](install-net-analyzers.md)。 请注意，无需更改项目的目标平台。

3. 启用其他规则：`Microsoft.CodeAnalysis.NetAnalyzers` 与 `Microsoft.CodeAnalysis.FxCopAnalyzers` 相比要传统得多。 与 FxCopAnalyzers 包不同，它只有几个正确性规则，这些规则[默认作为生成警告启用](/dotnet/fundamentals/code-analysis/overview#enabled-rules)。 可以通过自定义 [AnalysisMode](/dotnet/core/project-sdk/msbuild-props#analysismode) MSBuild 属性来[启用其他规则](/dotnet/fundamentals/code-analysis/overview#enable-additional-rules)。 例如，如果将属性设置为 `AllEnabledByDefault`，将默认启用所有适用的 CA 规则作为生成警告。

   ```xml
   <PropertyGroup>
     <AnalysisMode>AllEnabledByDefault</AnalysisMode>
   </PropertyGroup>
   ```

## <a name="see-also"></a>另请参阅

- [源代码分析与传统分析](net-analyzers-faq.yml#what-s-the-difference-between-legacy-fxcop-and--net-analyzers-)
- [从旧版分析迁移到 .NET 分析器](migrate-from-legacy-analysis-to-net-analyzers.md)
- [启用或安装 .NET 分析器](install-net-analyzers.md)
- [有关 .NET 分析器的常见问题解答](net-analyzers-faq.yml)
- [配置 .NET 分析器](/dotnet/fundamentals/code-analysis/code-quality-rule-options)
