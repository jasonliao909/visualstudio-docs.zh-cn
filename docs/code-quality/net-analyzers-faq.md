---
title: FxCop 代码分析（二进制分析）和 .NET 分析器（源分析）
ms.date: 09/06/2018
description: 了解旧版 FxCop（二进制分析）和 .NET 分析器（源分析）在 Visual Studio 中的差异。 请参阅有关如何使用这些分析器的问题的解答。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis FAQ
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 951e9b951f1d90077fe29506e9c288fb19f2d5ff
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2021
ms.locfileid: "108800445"
---
# <a name="frequently-asked-questions-about-legacy-fxcop-and-net-analyzers"></a>有关旧版 FxCop 和 .NET 分析器的常见问题解答

在了解旧版 FxCop（二进制分析）和 .NET 分析器（源分析）之间的区别时可能会产生混淆。 本文旨在解决你可能遇到的一些问题。

## <a name="whats-the-difference-between-legacy-fxcop-and-net-analyzers"></a>旧版 FxCop 和 .NET 分析器之间有什么区别？

旧版 FxCop 在已编译的程序集上运行生成后分析。 它作为单独的可执行文件运行，名为 FxCopCmd.exe。 FxCopCmd.exe 加载已编译的程序集，运行代码分析，然后报告结果（或“诊断”）。

.NET 分析器基于 .NET Compiler Platform（“Roslyn”）。 你[可以从 .NET SDK 启用它们，或者将它们安装为 NuGet 包](install-net-analyzers.md)，该包为项目或解决方案所引用。 分析器在编译器执行期间运行基于源代码的分析。 分析器托管在编译器进程（csc.exe 或 vbc.exe）中，并在生成项目时运行分析 。 报告分析器结果以及编译器结果。

## <a name="whats-the-difference-between-fxcop-analyzers-and-net-analyzers"></a>FxCop 分析器和 .NET 分析器之间有什么区别？

FxCop 分析器和 .NET 分析器都是指 .NET Compiler Platform ("Roslyn") 对 FxCop CA 规则的分析器实现。 在低于 Visual Studio 2019 16.8 和 .NET 5.0 的版本中，这些分析器作为 `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)提供。 从 Visual Studio 2019 16.8 和 .NET 5.0 开始，这些分析器[包含在 .NET SDK 中](/dotnet/fundamentals/code-analysis/overview)。 它们也作为 `Microsoft.CodeAnalysis.NetAnalyzers`[NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)提供。 请考虑[从 FxCop 分析器迁移到 .NET 分析器](migrate-from-fxcop-analyzers-to-net-analyzers.md)。

## <a name="does-the-run-code-analysis-command-run-net-analyzers"></a>“运行代码分析”命令是否运行 .NET 分析器？

在 Visual Studio 2019 16.5 版本之前，选择“分析” > “运行代码分析”时，它会执行旧式分析 。 从 Visual Studio 2019 16.5 开始，“运行代码分析”菜单选项会针对所选项目或解决方案执行基于 Roslyn 的分析器。 如果已安装 .NET 分析器，也会执行这些分析器。 有关详细信息，请参阅[如何：手动运行托管代码的代码分析](how-to-run-code-analysis-manually-for-managed-code.md)。

## <a name="does-the-runcodeanalysis-msbuild-project-property-run-analyzers"></a>RunCodeAnalysis msbuild 项目属性是否运行分析器？

不是。 项目文件（例如 .csproj）中的 RunCodeAnalysis 属性仅用于执行旧版 FxCop。 它将运行调用 FxCopCmd.exe 的生成后 msbuild 任务。

## <a name="so-how-do-i-run-net-analyzers-then"></a>那么我该如何运行 .NET 分析器呢？

若要运行 .NET 分析器，请首先[从 .NET SDK 启用它们，或将其安装为 NuGet 包](install-net-analyzers.md)。 然后在 Visual Studio 中或使用 msbuild 生成项目或解决方案。 Roslyn 分析器生成的警告和错误将显示在“错误列表”或命令窗口中。

## <a name="i-get-warning-ca0507-even-after-ive-installed-the-net-analyzers-nuget-package"></a>即使在安装了 .NET 分析器 NuGet 包之后，我仍会收到 CA0507 警告

如果已安装 .NET 分析器，但继续收到“‘运行代码分析’已被弃用，以支持在生成期间运行的 FxCop 分析器”的 CA0507 警告，可能需要将[项目文件](../ide/solutions-and-projects-in-visual-studio.md#project-file)中的“RunCodeAnalysis”msbuild 属性设置为“false”  。 否则，每次生成后将执行旧式分析。

```xml
<RunCodeAnalysis>false</RunCodeAnalysis>
```

## <a name="which-rules-have-been-ported-to-net-analyzers"></a>哪些规则已移植到 .NET 分析器中？

有关已移植到 .NET 分析器的旧分析规则的信息，请参阅 [Fxcop 规则端口状态](fxcop-rule-port-status.md)。

## <a name="code-analysis-warnings-are-treated-as-errors"></a>代码分析警告被视为错误

如果项目使用生成选项将警告视为错误，分析器警告可能会显示为错误。 要防止代码分析警告被视为错误，请执行[代码分析 FAQ](../code-quality/analyzers-faq.md#treat-warnings-as-errors) 中的步骤。

## <a name="see-also"></a>另请参阅

- [.NET Compiler Platform 分析器概述](roslyn-analyzers-overview.md)
- [迁移到 .NET 分析器](migrate-from-legacy-analysis-to-net-analyzers.md)
- [安装 .NET 分析器](install-net-analyzers.md)
