---
title: 从 FxCop 迁移到源代码分析（.NET 分析器）
ms.custom: SEO-VS-2020
description: 了解如何首次分析代码或如何从二进制分析 (FxCop) 迁移到使用源代码分析（.NET 分析器）分析托管代码的新方法。
ms.date: 09/17/2021
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
ms.openlocfilehash: c1cdffdd0970818f19a07c188cee7a75711e73e3
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128427390"
---
# <a name="migrate-from-legacy-analysis-fxcop-to-source-analysis-net-analyzers"></a>从传统分析 (FxCop) 迁移到源代码分析（.NET 分析器）

.NET Compiler Platform（“Roslyn”）分析器的源代码分析取代了托管代码的[传统分析](../code-quality/code-analysis-for-managed-code-overview.md)。 对于更新的项目模板（如 .NET Core 和 .NET Standard 项目），传统分析不可用。

许多传统分析 (FxCop) 规则已经针对 .NET 分析器（一组 Roslyn 代码分析器）进行了重写。 Roslyn 分析器在编译器执行期间运行基于源代码的分析。 报告分析器结果以及编译器结果。

有关传统分析与源代码分析之间的差异的详细信息，请参阅以下内容：

- [源代码分析与传统分析](../code-quality/net-analyzers-faq.yml#what-s-the-difference-between-legacy-fxcop-and--net-analyzers-)

- [有关 .NET 分析器的常见问题解答](../code-quality/net-analyzers-faq.yml)

## <a name="migration"></a>迁移

若要迁移到源代码分析，请执行以下操作：

1. [启用或安装 .NET 分析器](install-net-analyzers.md)。 与传统的分析规则冲突一样，源代码分析冲突会出现在 Visual Studio 的“错误列表”窗口中。 此外，源代码分析冲突也会在代码编辑器中显示，表现为违规代码下有波浪线。 规则的[严重性设置](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)决定波浪线的颜色。 若要查看移植到新 .NET 分析器的规则的状态，请参阅[移植和取消移植规则](../code-quality/fxcop-rule-port-status.md)。

   > [!NOTE]
   > 在低于 Visual Studio 2019 16.8 和 .NET 5.0 的版本中，这些分析器作为 `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)提供。 从 Visual Studio 2019 16.8 和 .NET 5.0 开始，这些分析器[包含在 .NET SDK 中](/dotnet/fundamentals/code-analysis/overview)。 它们也作为 `Microsoft.CodeAnalysis.NetAnalyzers`[NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)提供。 有关详细信息，请参阅[从 FxCop 分析器迁移到 .NET 分析器](migrate-from-fxcop-analyzers-to-net-analyzers.md)。

1. 若要解决 CA0507，请确保已为项目禁用旧版代码分析。 在项目文件中，将 `RunCodeAnalysis` 属性设置为 false：

   `<RunCodeAnalysis>false</RunCodeAnalysis>`

   或者，打开“项目属性” > “代码分析”，并禁用“生成时运行”设置。

## <a name="configuration"></a>Configuration

若要详细了解如何配置 .NET 分析器，请执行以下操作：

- 若要配置 .NET 分析器，请参阅[配置 .net 分析器](/dotnet/fundamentals/code-analysis/code-quality-rule-options)。

- 若要了解如何使用预定义的规则和 EditorConfig 或规则集文件来配置分析器，请参阅[启用规则类别](/dotnet/fundamentals/code-analysis/code-quality-rule-options)。

## <a name="see-also"></a>另请参阅

- [从 FxCop 分析器迁移到 .NET 分析器](migrate-from-fxcop-analyzers-to-net-analyzers.md)
