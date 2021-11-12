---
title: EditorConfig 与分析器
ms.date: 03/11/2019
description: 了解 Visual Studio 中基于 .NET Compiler Platform 的代码分析。 请参阅有关 EditorConfig 文件、规则集和其他主题的问题的解答。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2021
ms.locfileid: "108800446"
---
# <a name="code-analysis-faq"></a>代码分析常见问题解答

本页包含有关 Visual Studio 中基于 .NET Compiler Platform 的代码分析的一些常见问题解答。

## <a name="code-analysis-versus-editorconfig"></a>代码分析与 EditorConfig

**问**：应该使用代码分析还是 EditorConfig 来检查代码样式？

**答**：代码分析与 EditorConfig 文件协同工作。 在 [EditorConfig 文件](/dotnet/fundamentals/code-analysis/code-style-rule-options)或[“文本编辑器”选项](../ide/code-styles-and-code-cleanup.md)页面中定义代码样式时，实际上是在配置 Visual Studio 内置的代码分析器。 EditorConfig 文件可用于启用或禁用分析器规则，还可用于配置 NuGet 分析器包。

## <a name="editorconfig-versus-rule-sets"></a>EditorConfig 与规则集

**问**：应该使用规则集还是 EditorConfig 文件配置分析器？

**答**：规则集和 EditorConfig 文件可以共存，并可同时用于配置分析器。 EditorConfig 文件和规则集都可用于启用和禁用规则，并设置其严重性。

但是，EditorConfig 文件还提供了其他规则配置方法：

- 对于 .NET 代码质量分析器，EditorConfig 文件允许[定义要分析的代码类型](/dotnet/fundamentals/code-analysis/code-quality-rule-options)。
- 对于 Visual Studio 内置的 .NET 代码样式分析器，你可以使用 EditorConfig 文件[为代码库定义首选代码样式](/dotnet/fundamentals/code-analysis/code-style-rule-options)。

除了规则集和 EditorConfig 文件之外，还通过使用标记为 C# 和 VB 编译器的[其他文件](../ide/build-actions.md#build-action-values)的文本文件来配置某些分析器。

> [!NOTE]
> - EditorConfig 文件只能用于启用规则，并在 Visual Studio 2019 版本 16.3 及更高版本中设置其严重性。
> - 不能使用 EditorConfig 文件来配置旧分析，但可以使用规则集来配置。

## <a name="code-analysis-in-ci-builds"></a>CI 生成中的代码分析

**问**：在持续集成 (CI) 生成中，基于 .NET Compiler Platform 的代码分析是否起作用？

**答**：是的。 对于从 NuGet 包安装的分析器，这些规则[在生成时强制执行](roslyn-analyzers-overview.md#build-errors)，包括在 CI 生成过程中。 CI 生成中使用的分析器遵循规则集和 EditorConfig 文件中的规则配置。 目前，Visual Studio 中内置的代码分析器不作为 NuGet 包提供，因此在 CI 生成中无法强制执行这些规则。

## <a name="ide-analyzers-versus-stylecop"></a>IDE 分析器与 StyleCop

**问**：Visual Studio IDE 代码分析器与 StyleCop 分析器有何区别？

**答**：Visual Studio IDE 包含内置分析器，用于查找代码样式和质量问题。 这些规则可帮助你在引入新的语言功能时使用它们，并改进代码的可维护性。 IDE 分析器随每个 Visual Studio 版本不断更新。

[StyleCop 分析器](https://github.com/DotNetAnalyzers/StyleCopAnalyzers)是作为 NuGet 包安装的第三方分析器，用于检查代码中的样式一致性。 通常，StyleCop 规则允许你为代码库设置个人首选项，而不是推荐一种样式而不推荐另一种。

## <a name="code-analyzers-versus-legacy-analysis"></a>代码分析器与旧分析

**问**：旧分析与基于 .NET Compiler Platform 的代码分析有何区别？

**答**：基于 .NET Compiler Platform 的代码分析可在编译过程中实时分析源代码，而旧分析则在生成完成后分析二进制文件。 有关详细信息，请参阅[基于 .NET Compiler Platform 的分析与旧分析](../code-quality/net-analyzers-faq.md#whats-the-difference-between-legacy-fxcop-and-net-analyzers)。

## <a name="fxcop-analyzers-versus-net-analyzers"></a>FxCop 分析器与 .NET 分析器

**问**：FxCop 分析器和 .NET 分析器之间有什么区别？

**答**：FxCop 分析器和 .NET 分析器都是指 .NET Compiler Platform ("Roslyn") 对 FxCop CA 规则的分析器实现。 在低于 Visual Studio 2019 16.8 和 .NET 5.0 的版本中，这些分析器作为 `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)提供。 从 Visual Studio 2019 16.8 和 .NET 5.0 开始，这些分析器[包含在 .NET SDK 中](/dotnet/fundamentals/code-analysis/overview)。 它们也作为 `Microsoft.CodeAnalysis.NetAnalyzers`[NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)提供。 请考虑[从 FxCop 分析器迁移到 .NET 分析器](migrate-from-fxcop-analyzers-to-net-analyzers.md)。

## <a name="treat-warnings-as-errors"></a>视警告为错误

**问**：我的项目使用生成选项来将警告视为错误。 从旧分析迁移到源代码分析后，所有代码分析警告现在都将显示为错误。 如何防止出现这种情况？

**答**：要防止代码分析警告被视为错误，请执行以下步骤：

  1. 创建一个包含以下内容的 .props 文件：

     ```xml
     <Project>
        <PropertyGroup>
           <CodeAnalysisTreatWarningsAsErrors>false</CodeAnalysisTreatWarningsAsErrors>
        </PropertyGroup>
     </Project>
     ```

  2. 向 .csproj 或 .vbproj 项目文件添加一行，导入在上一步中创建的 .props 文件。 此行必须放在导入分析器 .props 文件的任何行之前。 例如，如果你的 .props 文件命名为 codeanalysis.props：

     ```xml
     ...
     <Import Project="..\..\codeanalysis.props" Condition="Exists('..\..\codeanalysis.props')" />
     <Import Project="..\packages\Microsoft.CodeAnalysis.NetAnalyzers.5.0.0\build\Microsoft.CodeAnalysis.NetAnalyzers.props" Condition="Exists('..\packages\Microsoft.CodeAnalysis.NetAnalyzers.5.0.0\build\Microsoft.CodeAnalysis.NetAnalyzers.props')" />
     ...
     ```

## <a name="code-analysis-solution-property-page"></a>代码分析解决方案属性页

**问**：解决方案的 Code Analysis 属性页在何处？

**答**：解决方案级别的 Code Analysis 属性页已删除，以支持更可靠的共享属性组。 对于在项目级别管理代码分析，Code Analysis 属性页仍可用。 （对于托管项目，我们还建议从规则集迁移到 EditorConfig，以便进行规则配置。）对于在解决方案或存储库中跨多个/所有项目共享规则集，我们建议使用共享属性/目标文件或 Directory.props/Directory.targets 文件中的 [CodeAnalysisRuleSet](../code-quality/using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project) 属性定义属性组。 如果你没有任何项目导入的公共属性或目标，则应考虑将此类属性组添加到顶级解决方案目录下的 [Directory.props 或 Directory.targets 文件](../msbuild/customize-your-build.md)中，该目录会自动导入到目录或其子目录中定义的所有项目文件中。

## <a name="see-also"></a>另请参阅

- [分析器概述](roslyn-analyzers-overview.md)
- [EditorConfig 的 .NET 编码约定设置](/dotnet/fundamentals/code-analysis/code-style-rule-options)