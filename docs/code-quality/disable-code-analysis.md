---
title: 关闭代码分析
ms.date: 09/01/2020
description: 了解如何在 .net Core、.NET Standard 和 .NET Framework 项目中关闭 Visual Studio 源代码分析。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- code analysis, disable
- disable code analysis
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.openlocfilehash: 8d86945cb39e1e6c37e62726b920ee774c0f7146
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122053053"
---
# <a name="disable-source-code-analysis-for-net"></a>禁用 .NET 源代码分析

::: moniker range=">=vs-2019"

此页可帮助你在 Visual Studio 中禁用代码分析。 您可以禁用的内容有限制，而关闭代码分析的过程会因几个因素而异：

- Project 类型 ( .net Core/Standard 与 .NET Framework) 

  .net Core 和 .NET Standard 项目在其 Code Analysis 属性页上有一些选项，可让你从安装为 NuGet 包的分析器关闭代码分析。 有关详细信息，请参阅 [.Net Core 和 .NET Standard 项目](#net-core-and-net-standard-projects)。 若要关闭 .NET Framework 项目的源代码分析，请参阅[.NET Framework 项目](#net-framework-projects)。

- 源分析与传统分析

  本主题适用于源代码分析，不适用于旧版 (二进制) 分析。 有关禁用旧分析的信息，请参阅 [如何：启用和禁用旧代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

## <a name="net-core-and-net-standard-projects"></a>.NET Core 和 .NET Standard 项目

从 Visual Studio 2019 16.3 版开始，Code Analysis 属性 "页中提供了两个复选框，可用于控制分析器是否在生成时和设计时运行。 这些选项特定于项目。

![在 Visual Studio 中启用或禁用实时代码分析或生成](media/run-on-build-run-live-analysis.png)

若要打开此页，请在 **解决方案资源管理器** 中右键单击项目节点，然后选择 " **属性**"。 选择 " **Code Analysis** " 选项卡。

- 若要在生成时禁用源分析，请取消选中 " **在生成上运行** " 选项。
- 若要禁用实时源分析，请取消选中 " **在实时分析上运行** " 选项。

> [!NOTE]
> 从 Visual Studio 2019 版16.5 开始，如果你喜欢按需代码分析执行工作流，则可以在实时分析和/或生成时禁用分析器执行，并按需在项目或解决方案上手动触发代码分析。 有关手动运行代码分析的信息，请参阅[如何：手动运行托管代码 Code Analysis](how-to-run-code-analysis-manually-for-managed-code.md)。

## <a name="net-framework-projects"></a>.NET Framework 项目

若要禁用分析器的源代码分析，请将以下一个或多个 MSBuild 属性添加到[项目文件](../ide/solutions-and-projects-in-visual-studio.md#project-file)。

| MSBuild 属性 | 说明 | 默认 |
| - | - | - |
| `RunAnalyzersDuringBuild` | 控制分析器是否在生成时运行。 | `true` |
| `RunAnalyzersDuringLiveAnalysis` | 控制分析器是否在设计时实时分析代码。 | `true` |
| `RunAnalyzers` | 在生成和设计时禁用分析器。 此属性优先于 `RunAnalyzersDuringBuild` 和 `RunAnalyzersDuringLiveAnalysis` 。 | `true` |

示例：

```xml
<RunAnalyzersDuringBuild>false</RunAnalyzersDuringBuild>
<RunAnalyzersDuringLiveAnalysis>false</RunAnalyzersDuringLiveAnalysis>
<RunAnalyzers>false</RunAnalyzers>
```

::: moniker-end

::: moniker range="vs-2017"

## <a name="source-analysis"></a>源分析

无法在 Visual Studio 2017 中关闭[源分析](roslyn-analyzers-overview.md)。 如果要从 **错误列表** 中清除分析器错误，可以通过选择 "**分析**  >  运行" Code Analysis 并在菜单栏上 **取消显示活动问题** 来禁止所有当前冲突。 有关详细信息，请参阅[抑制冲突](use-roslyn-analyzers.md#suppress-violations)。

从 Visual Studio 2019 16.3 版开始，可以关闭源代码分析或按需执行。 请考虑升级到 Visual Studio 2019。

## <a name="legacy-analysis"></a>旧版分析

您可以在 " **Code Analysis** 属性" 页上禁用旧的生成时分析。 有关详细信息，请参阅 [如何：启用和禁用旧代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

::: moniker-end

## <a name="see-also"></a>请参阅

- [禁止冲突](use-roslyn-analyzers.md#suppress-violations)
- [如何：启用和禁用旧代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
