---
title: EditorConfig 与分析器
ms.date: 03/11/2019
description: 了解.NET Compiler Platform中基于代码Visual Studio。 查看有关 EditorConfig 文件、规则集和其他主题的问题的答案。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- analyzers, faq
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6d67471027f36d0e22c055f4306ce2137d972463
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2021
ms.locfileid: "108800446"
---
# <a name="code-analysis-faq"></a>代码分析常见问题解答

本页包含有关 .NET Compiler Platform 中基于代码分析的一些常见问题Visual Studio。

## <a name="code-analysis-versus-editorconfig"></a>代码分析与 EditorConfig

**问**：我应该使用代码分析还是 EditorConfig 来检查代码样式？

**答**：代码分析和 EditorConfig 文件可同时工作。 在[EditorConfig 文件或](/dotnet/fundamentals/code-analysis/code-style-rule-options)文本编辑器"选项"页上定义[](../ide/code-styles-and-code-cleanup.md)代码样式时，实际上是在配置内置于编辑器Visual Studio。 EditorConfig 文件可用于启用或禁用分析器规则，还可用于配置 NuGet 分析器包。

## <a name="editorconfig-versus-rule-sets"></a>EditorConfig 与规则集

**问**：我应该使用规则集还是 EditorConfig 文件配置分析器？

**答**：规则集和 EditorConfig 文件可以共存，并可用于配置分析器。 EditorConfig 文件和规则集都允许启用和禁用规则并设置其严重性。

但是，EditorConfig 文件还提供其他方法来配置规则：

- 对于 .NET 代码质量分析器，EditorConfig 文件允许 [定义要分析的代码类型](/dotnet/fundamentals/code-analysis/code-quality-rule-options)。
- 对于内置于 Visual Studio 中的 .NET 代码样式分析器，EditorConfig 文件允许定义基本 [代码的首选代码](/dotnet/fundamentals/code-analysis/code-style-rule-options) 样式。

除了规则集和 EditorConfig 文件外，某些分析器还使用标记为 C# 和 VB 编译器的其他文件的文本文件进行配置。 [](../ide/build-actions.md#build-action-values)

> [!NOTE]
> - EditorConfig 文件只能用于在 2019 Visual Studio 16.3 及更高版本中启用规则并设置其严重性。
> - EditorConfig 文件不能用于配置旧分析，而规则集可以。

## <a name="code-analysis-in-ci-builds"></a>CI 生成中的代码分析

**问**：基于 .NET Compiler Platform 的代码分析是否在持续集成 (CI) 生成？

**答**：是的。 对于从 NuGet 包安装的分析器，将 [在生成时强制执行](roslyn-analyzers-overview.md#build-errors)这些规则，包括在 CI 生成过程中。 CI 生成中使用的分析器遵循规则集和 EditorConfig 文件中的规则配置。 目前，Visual Studio 中内置的代码分析器不作为 NuGet 包提供，因此在 CI 生成中无法强制执行这些规则。

## <a name="ide-analyzers-versus-stylecop"></a>IDE 分析器与 StyleCop

**问**： VISUAL Studio IDE 代码分析器和 StyleCop 分析器之间有何区别？

**答**： VISUAL Studio IDE 包含内置分析器，用于查找代码样式和质量问题。 这些规则可帮助你在引入新语言功能时使用它们，并改进代码的可维护性。 IDE 分析器随每个 Visual Studio 版本不断地进行更新。

[StyleCop 分析器](https://github.com/DotNetAnalyzers/StyleCopAnalyzers) 是作为 NuGet 包安装的第三方分析器，用于检查代码中的样式一致性。 通常，StyleCop 规则允许你为基本代码设置个人首选项，而无需对另一种样式进行建议。

## <a name="code-analyzers-versus-legacy-analysis"></a>代码分析器与传统分析

**问**：传统分析和基于 .NET Compiler Platform 的代码分析之间有何区别？

**答**：基于 .NET Compiler Platform 的代码分析实时分析源代码，并在编译期间分析二进制文件。 有关详细信息，请参阅 [基于 .NET Compiler Platform 的分析与旧式分析](../code-quality/net-analyzers-faq.md#whats-the-difference-between-legacy-fxcop-and-net-analyzers)。

## <a name="fxcop-analyzers-versus-net-analyzers"></a>FxCop 分析器与 .NET 分析器

**问**： FxCop 分析器与 .net 分析器之间有何区别？

**答**： fxcop 分析器和 .Net 分析器都是指 fxcop CA 规则 ) 分析器实现的 .NET Compiler Platform ( "Roslyn"。 在 Visual Studio 2019 16.8 和 .NET 5.0 之前，这些分析器作为 `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)提供。 从 Visual Studio 2019 16.8 和 .NET 5.0 开始，这些分析器 [包含在 .NET SDK 中](/dotnet/fundamentals/code-analysis/overview)。 它们还作为 `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet 包 提供](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)。 请考虑 [从 FxCop 分析器迁移到 .NET 分析器](migrate-from-fxcop-analyzers-to-net-analyzers.md)。

## <a name="treat-warnings-as-errors"></a>视警告为错误

**问**：我的项目使用生成选项将警告视为错误。 从旧分析迁移到源代码分析后，所有代码分析警告现在都显示为错误。 如何防止这种情况？

**答**：若要防止将代码分析警告视为错误，请执行以下步骤：

  1. 创建包含以下内容的 .props 文件：

     ```xml
     <Project>
        <PropertyGroup>
           <CodeAnalysisTreatWarningsAsErrors>false</CodeAnalysisTreatWarningsAsErrors>
        </PropertyGroup>
     </Project>
     ```

  2. 向 .csproj 或 .vbproj 项目文件添加一行，以导入在上一步中创建的 .props 文件。 此行必须放置在导入分析器 .props 文件的任何行之前。 例如，如果 .props 文件名为 codeanalysis.props：

     ```xml
     ...
     <Import Project="..\..\codeanalysis.props" Condition="Exists('..\..\codeanalysis.props')" />
     <Import Project="..\packages\Microsoft.CodeAnalysis.NetAnalyzers.5.0.0\build\Microsoft.CodeAnalysis.NetAnalyzers.props" Condition="Exists('..\packages\Microsoft.CodeAnalysis.NetAnalyzers.5.0.0\build\Microsoft.CodeAnalysis.NetAnalyzers.props')" />
     ...
     ```

## <a name="code-analysis-solution-property-page"></a>代码分析解决方案属性页

**问**：解决方案的Code Analysis属性页在哪里？

**答**：Code Analysis删除解决方案级别的属性页，以支持更可靠的共享属性组。 为了Code Analysis级别管理项目级别，Code Analysis属性页仍然可用。  (对于托管项目，我们还建议从规则集迁移到 EditorConfig 进行规则配置。) 若要跨解决方案或存储库的多个/所有项目共享规则集，建议在共享属性/目标文件或 *Directory.props/Directory.targets* 文件中定义具有 [CodeAnalysisRuleSet](../code-quality/using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project)属性的属性组。 如果没有所有项目导入的任何此类常见属性或目标，应考虑将此类属性组添加到顶级解决方案目录中的 [Directory.props 或 Directory.targets](../msbuild/customize-your-build.md) 文件，该文件会自动导入目录及其子目录中定义的所有项目文件中。

## <a name="see-also"></a>请参阅

- [分析器概述](roslyn-analyzers-overview.md)
- [EditorConfig 的 .NET 编码约定设置](/dotnet/fundamentals/code-analysis/code-style-rule-options)