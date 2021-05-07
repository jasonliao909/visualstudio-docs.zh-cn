---
title: '从 FxCop 迁移到源分析 (.NET 分析器) '
ms.custom: SEO-VS-2020
description: 了解如何首次分析代码，或者如何从二进制分析 (FxCop) 迁移到使用源分析 (.NET 分析器分析托管代码的新) 。
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
ms.openlocfilehash: 9a673e7467816e71b8240de9e5f68840c9188dcd
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798227"
---
# <a name="migrate-from-legacy-analysis-fxcop-to-source-analysis-net-analyzers"></a>从旧版分析 (FxCop) 迁移到源分析 (.NET 分析器) 

"Roslyn".NET Compiler Platform (分析器) 替换 [托管代码的旧](../code-quality/code-analysis-for-managed-code-overview.md) 分析。 对于较新的项目模板（如 .NET Core 和 .NET Standard，旧分析不可用。

许多旧版 FxCop (规则) .NET 分析器（一组 Roslyn 代码分析器）已重写。 Roslyn 分析器在编译器执行期间运行基于源代码的分析。 报告分析器结果以及编译器结果。

有关旧分析和源分析之间的差异详细信息，请参阅以下内容：

- [源代码分析与传统分析](../code-quality/net-analyzers-faq.yml#what-s-the-difference-between-legacy-fxcop-and--net-analyzers-)

- [有关 .NET 分析器常见问题解答](../code-quality/net-analyzers-faq.yml)

## <a name="migration"></a>迁移

若要迁移到源分析， [请启用或安装 .NET 分析器](install-net-analyzers.md)。 与传统的分析规则冲突一样，源代码分析冲突会出现在 Visual Studio 的“错误列表”窗口中。 此外，源代码分析冲突也会在代码编辑器中显示，表现为违规代码下有波浪线。 规则的[严重性设置](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)决定波浪线的颜色。 若要查看移植到新的 .NET 分析器的规则的状态，请参阅 [移植和未移植的规则](../code-quality/fxcop-rule-port-status.md)。

> [!NOTE]
> 在 2019 Visual Studio 16.8 和 .NET 5.0 之前，这些分析器作为 `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)包 提供。 从 Visual Studio 2019 16.8 和 .NET 5.0 开始，这些分析器 [包含在 .NET SDK 中](/dotnet/fundamentals/code-analysis/overview)。 它们还作为 `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet 包 提供](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)。 有关详细信息，请参阅从 [FxCop 分析器迁移到 .NET 分析器](migrate-from-fxcop-analyzers-to-net-analyzers.md)。

## <a name="configuration"></a>配置

若要详细了解如何配置 .NET 分析器，请执行以下操作：

- 若要配置 .NET 分析器，请参阅 [配置 .NET 分析器](/dotnet/fundamentals/code-analysis/code-quality-rule-options)。

- 若要了解如何将预定义规则与 EditorConfig 或规则集文件一起配置分析器，请参阅启用 [规则类别](/dotnet/fundamentals/code-analysis/code-quality-rule-options)。

## <a name="see-also"></a>请参阅

- [从 FxCop 分析器迁移到 .NET 分析器](migrate-from-fxcop-analyzers-to-net-analyzers.md)
