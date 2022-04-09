---
title: 使用 Roslyn 分析器进行代码分析
ms.date: 01/15/2022
description: 熟悉 Visual Studio 中的源代码分析。 了解代码修补程序以及不同类型的分析器和严重性级别。
ms.custom: SEO-VS-2020, devdivchpfy22
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
- code analyzers
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: 542b900fecdcd1296db1ce37e553a4a7eb35b098
ms.sourcegitcommit: 015d0bf8295f48d687c91aacc4ec2747063fe9ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2022
ms.locfileid: "141533288"
---
# <a name="overview-of-source-code-analysis"></a>源代码分析概述

.NET Compiler Platform (Roslyn) 分析器检查 C# 或 Visual Basic 代码的样式、质量、可维护性、设计及其他问题。 此检查或分析在所有打开的文件的设计期间发生。

分析器分为以下组：

- [代码样式](/dotnet/fundamentals/code-analysis/code-style-rule-options?preserve-view=true&view=vs-2019#convention-categories)分析器内置于Visual Studio中。 分析器的诊断 ID 或代码格式为 IDExxxx，例如 IDE0067。 可以在[文本编辑器选项页](../ide/code-styles-and-code-cleanup.md)上或在 [EditorConfig 文件](/dotnet/fundamentals/code-analysis/code-style-rule-options)中配置首选项。 从 .NET 5.0 开始，代码样式分析器包含在 .NET SDK 中，并且可以作为生成警告或错误严格地强制实施。 有关详细信息，请参阅 [.NET 源代码分析概述](/dotnet/fundamentals/productivity/code-analysis#code-style-analysis)。

- 现在，[代码质量](/dotnet/fundamentals/code-analysis/quality-rules/index)分析器包含在 .NET 5 SDK 中并且在默认情况下已启用。 分析器的诊断 ID 或代码格式为 CAxxxx，例如 CA1822。 有关详细信息，请参阅 [.NET 代码质量分析概述](/dotnet/fundamentals/productivity/code-analysis#code-quality-analysis)。

- 可以将外部分析器（如 [StyleCop](https://www.nuget.org/packages/StyleCop.Analyzers/)、[Roslynator](https://www.nuget.org/packages/Roslynator.Analyzers/)、[XUnit Analyzers](https://www.nuget.org/packages/xunit.analyzers/) 和 [Sonar Analyzer](https://www.nuget.org/packages/SonarAnalyzer.CSharp/)）安装为NuGet包或Visual Studio扩展。

## <a name="severity-levels-of-analyzers"></a>分析器的严重性级别

每个分析器都具有以下严重性级别之一：

| 严重性（解决方案资源管理器） | 严重性（EditorConfig 文件） | 生成时行为 | 编辑器行为 |
|-|-|-|
| 错误 | `error` | 此类冲突在错误列表和命令行生成输出中显示为“错误”，并导致生成失败。| 冒犯代码用红色波浪线下划线，并用滚动条中的小红色框标记。 |
| 警告 | `warning` | 冲突在错误列表和命令行生成输出中显示为 *警告* ，但不会导致生成失败。 | 冒犯代码用绿色波浪线下划线，并用滚动条中的小绿色框标记。 |
| 信息 | `suggestion` | 此类冲突在错误列表中显示为“消息”，而不会在命令行生成输出中显示。 | 冒犯代码用灰色波浪线下划线，并用滚动条中的小灰色框标记。 |
| Hidden | `silent` | 对用户不可见。 | 对用户不可见。 但是，诊断会报告给 IDE 诊断引擎。 |
| 无 | `none` | 完全禁止显示。 | 完全禁止显示。 |
| 默认 | `default` | 对应于规则的默认严重性。 若要确定规则的默认值，请查看“属性”窗口。 | 对应于规则的默认严重性。 |

如果分析器发现规则冲突，则会在代码编辑器中报告这些冲突，在冒犯代码和错误列表窗口中将其报告为 *波浪* 线。

![“错误列表”窗口中的分析器冲突](../code-quality/media/code-analysis-error-list.png)

错误列表中报告的分析器冲突与规则的[严重性级别设置](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)相匹配。 分析器冲突也会在代码编辑器中以波浪线的形式显示在违规代码下。 下图显示了三个冲突&mdash;一个错误（红色波浪线）、一个警告（绿色波浪线）和一个建议（三个灰点）：

![Visual Studio 中代码编辑器中的波浪线](media/diagnostics-severity-colors.png)

许多分析器规则或诊断都有一个或多个相关的代码修复程序，可以应用它们来纠正规则冲突。 代码修复以及其他类型的[快速操作](../ide/quick-actions.md)显示在灯泡图标菜单中。 有关这些代码修复的信息，请参阅[常见快速操作](../ide/quick-actions.md)。

![分析器冲突和快速操作代码修复](../code-quality/media/built-in-analyzer-code-fix.png)

## <a name="configure-analyzer-severity-levels"></a>配置分析器严重性级别

可以在 [EditorConfig 文件](../code-quality/use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file)中或从[灯泡菜单](../code-quality/use-roslyn-analyzers.md#set-rule-severity-from-the-light-bulb-menu)中配置分析器规则的严重性或诊断。

分析器还可以配置为在生成时检查代码，并在键入时保持运行状态。 你可配置实时代码分析的范围，以仅对当前文档执行、对所有打开的文档执行或对整个解决方案执行。 请参阅[如何：配置实时代码分析范围](./configure-live-code-analysis-scope-managed-code.md)。

> [!TIP]
> 仅当分析器作为 NuGet 包安装时，才会显示来自代码分析器的生成时错误和警告。 内置分析器（例如 IDE0067 和 IDE0068）不会在生成期间运行。

## <a name="nuget-package-versus-vsix-extension"></a>NuGet 包与 VSIX 扩展

可以通过NuGet包为每个项目安装外部分析器。 有些还可用作Visual Studio扩展，在这种情况下，它们适用于在Visual Studio中打开的任何解决方案。 这两种[安装分析器](../code-quality/install-roslyn-analyzers.md)方法之间存在一些关键行为差异。

### <a name="scope"></a>范围

如果将分析器安装为 Visual Studio 扩展，则它们将在解决方案级别应用于 Visual Studio 的所有实例。 如果将分析器安装为 NuGet 包（这是首选方法），它们仅适用于安装了 NuGet 软件包的项目。 在团队环境中，作为 NuGet 包安装的分析器适用于处理该项目的所有开发人员。

> [!NOTE]
> 第一方分析器还会在 .NET SDK 内部提供。 建议尽可能从 .NET SDK 启用这些分析器，而不是安装`Microsoft.CodeAnalysis.NetAnalyzers`[NuGet包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)。 从 .NET SDK 启用分析器可以确保在更新 SDK 后，立即自动获取分析器 bug 修复和新分析器。 有关更多详细信息 [，请参阅"启用或安装第一方 .NET 分析器](install-net-analyzers.md) "。

### <a name="build-errors"></a>生成错误

若要在生成时强制实施规则，包括通过命令行或作为持续集成 (CI) 生成的一部分，请选择以下选项之一：

- 创建一个 .NET 5.0 或更高版本的项目，该项目默认在 .NET SDK 中包含分析器。 代码分析功能针对面向 .NET 5.0 或更高版本的项目默认启用。 可通过将 [EnableNETAnalyzers](/dotnet/core/project-sdk/msbuild-props#enablenetanalyzers) 属性设置为 true，在面向 .NET 早期版本的项目上启用代码分析。

- 将分析器安装为 NuGet 包。 如果将分析器作为扩展安装，则分析器警告和错误不会显示在生成报告中。

以下图像显示了生成包含分析器规则冲突的项目时的命令行生成输出：

![带规则冲突的 MSBuild 输出](media/command-line-build-analyzers.png)

### <a name="rule-severity"></a>规则严重性

无法从作为Visual Studio扩展安装的分析器配置规则的严重性。 若要配置[规则严重性](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)，则应将分析器安装为 NuGet 包。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [在 Visual Studio 中安装代码分析器](../code-quality/install-roslyn-analyzers.md)

> [!div class="nextstepaction"]
> [在 Visual Studio 中使用代码分析器](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>请参阅

- [分析器常见问题解答](analyzers-faq.yml)
- [编写自己的代码分析器](../extensibility/getting-started-with-roslyn-analyzers.md)
- [.NET 编译器平台 SDK](/dotnet/csharp/roslyn-sdk/)