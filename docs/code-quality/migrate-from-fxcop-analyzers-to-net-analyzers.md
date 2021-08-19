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
ms.technology: vs-ide-code-analysis
ms.openlocfilehash: ba0b545b41c3c23bef93b7dee86b0f188a01a7cd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122122106"
---
# <a name="migrate-from-fxcop-analyzers-to-net-analyzers"></a>从 FxCop 分析器迁移到 .NET 分析器

.NET Compiler Platform ( "Roslyn" 的源分析 ) 分析器替换托管代码的[旧式分析](code-analysis-for-managed-code-overview.md)。 许多旧分析 (FxCop) 规则已经重新编写为源分析器。

在 2019 16.8 和 .net 5.0 Visual Studio 之前，这些分析器作为 `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)附带。

从 Visual Studio 2019 16.8 和 .net 5.0 开始， [.net SDK 中提供](/dotnet/fundamentals/code-analysis/overview)了这些分析器。 如果不想移到 .net 5 + SDK，或者想要使用基于 NuGet 包的模型，也可以在 `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)中使用该分析器。 对于按需版本更新，你可能更倾向于使用基于包的模型。

> [!NOTE]
> 第一方 .NET 分析器与目标平台无关。 也就是说，你的项目不需要面向特定的 .NET 平台。 分析器适用于目标为的项目以及 `net5.0` 更早的 .net 版本，如 `netcoreapp` 、 `netstandard` 和 `net472` 。

## <a name="migration-steps"></a>迁移步骤

从版本开始 `3.3.2` ， `Microsoft.CodeAnalysis.FxCopAnalyzers` NuGet 包已弃用。 请按照以下步骤将你的项目或解决方案从迁移 `Microsoft.CodeAnalysis.FxCopAnalyzers` 到 .net 分析器：

1. 卸载 `Microsoft.CodeAnalysis.FxCopAnalyzers` NuGet 包

2. [启用或安装 .net 分析器](install-net-analyzers.md)。 请注意，不需要更改项目的目标平台。

3. 启用其他规则： `Microsoft.CodeAnalysis.NetAnalyzers` 与相比，更保守 `Microsoft.CodeAnalysis.FxCopAnalyzers` 。 与 FxCopAnalyzers 包不同，它仅有几个在 [默认情况下启用为生成警告](/dotnet/fundamentals/code-analysis/overview#enabled-rules)的正确性规则。 您可以通过自定义[AnalysisMode](/dotnet/core/project-sdk/msbuild-props#analysismode) MSBuild 属性来[启用其他规则](/dotnet/fundamentals/code-analysis/overview#enable-additional-rules)。 例如，如果将属性设置为，则 `AllEnabledByDefault` 默认情况下会启用所有适用的 CA 规则作为生成警告。

   ```xml
   <PropertyGroup>
     <AnalysisMode>AllEnabledByDefault</AnalysisMode>
   </PropertyGroup>
   ```

## <a name="see-also"></a>请参阅

- [源代码分析与传统分析](net-analyzers-faq.yml#what-s-the-difference-between-legacy-fxcop-and--net-analyzers-)
- [从旧版分析迁移到 .NET 分析器](migrate-from-legacy-analysis-to-net-analyzers.md)
- [启用或安装 .NET 分析器](install-net-analyzers.md)
- [.NET 分析器常见问题](net-analyzers-faq.yml)
- [配置 .NET 分析器](/dotnet/fundamentals/code-analysis/code-quality-rule-options)
