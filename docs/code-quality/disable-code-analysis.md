---
title: 关闭代码分析
ms.date: 01/20/2022
description: 了解如何在 .NET Core、.NET Standard 和 .NET Framework 项目中关闭 Visual Studio 源代码分析。
ms.custom: SEO-VS-2020, devdivchpfy22
ms.topic: how-to
helpviewer_keywords:
- code analysis, disable
- disable code analysis
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.openlocfilehash: fdfa36298af77197d287374929d9d90e66e09e2a
ms.sourcegitcommit: 20f9529648e69707063dccb2b15089bf4e9bf639
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2022
ms.locfileid: "137886459"
---
# <a name="disable-source-code-analysis-for-net"></a>禁用 .NET 的源代码分析

::: moniker range=">=vs-2022"

此页可帮助你禁用 Visual Studio 中的代码分析。 你可以禁用的内容有限制，而关闭代码分析的过程会因几个因素而异：

- 项目类型（.NET Core/Standard 与 .NET Framework）

  .NET Core 和 .NET Standard 项目在其“代码分析”属性页上有一些选项，可让你从作为 NuGet 包安装的分析器中关闭代码分析。 有关详细信息，请参阅 [.NET Core 和 .NET Standard 项目](#net-core-and-net-standard-projects)。 若要关闭 .NET Framework 项目的源代码分析，请参阅 [.NET Framework 项目](#net-framework-projects)。

- 源分析与旧版分析

  本文适用于源代码分析，而适用于旧版 (二进制) 分析。 有关禁用旧版分析的信息，请参阅[如何：启用和禁用旧版代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

## <a name="net-core-and-net-standard-projects"></a>.NET Core 和 .NET Standard 项目

从 Visual Studio 2022 版本 17.0.4 开始，Code Analysis 属性页中提供了两个复选框，可用于控制分析器是否在生成时和设计时运行。 这些选项特定于项目。

![在 Visual Studio 中启用或禁用实时代码分析或生成时的代码分析](media/run-on-build-run-live-analysis-1.png)

要打开该页面，右键单击“解决方案资源管理器”中的项目节点，然后选择“属性” 。 选择“代码分析”选项卡。

- 若要在生成时禁用源分析，请取消选中“在生成时运行”选项。
- 若要禁用实时源分析，请取消选中“在实时分析时运行”选项。

> [!NOTE]
> 从 Visual Studio 2022 版本 17.0.4 开始，如果你更喜欢按需代码分析执行工作流，可以在实时分析期间禁用分析器执行。 或者按需对项目或解决方案生成并手动触发代码分析一次。 有关手动运行代码分析的信息，请参阅[如何：手动运行托管代码的代码分析](how-to-run-code-analysis-manually-for-managed-code.md)。

## <a name="net-framework-projects"></a>.NET Framework 项目

若要关闭分析器的源代码分析，请将以下一个或多个 MSBuild 属性添加到[项目文件](../ide/solutions-and-projects-in-visual-studio.md#project-file)。

| MSBuild 属性 | 说明 | 默认 |
| - | - | - |
| `RunAnalyzersDuringBuild` | 控制分析器是否在生成时运行。 | `true` |
| `RunAnalyzersDuringLiveAnalysis` | 控制分析器是否在设计时实时分析代码。 | `true` |
| `RunAnalyzers` | 在生成时和设计时禁用分析器。 此属性优先于 `RunAnalyzersDuringBuild` 和 `RunAnalyzersDuringLiveAnalysis`。 | `true` |

示例：

```xml
<RunAnalyzersDuringBuild>false</RunAnalyzersDuringBuild>
<RunAnalyzersDuringLiveAnalysis>false</RunAnalyzersDuringLiveAnalysis>
<RunAnalyzers>false</RunAnalyzers>
```

::: moniker-end

::: moniker range="vs-2019"

此页可帮助你禁用 Visual Studio 中的代码分析。 你可以禁用的内容有限制，而关闭代码分析的过程会因几个因素而异：

- 项目类型（.NET Core/Standard 与 .NET Framework）

  .NET Core 和 .NET Standard 项目在其“代码分析”属性页上有一些选项，可让你从作为 NuGet 包安装的分析器中关闭代码分析。 有关详细信息，请参阅 [.NET Core 和 .NET Standard 项目](#net-core-and-net-standard-projects)。 若要关闭 .NET Framework 项目的源代码分析，请参阅 [.NET Framework 项目](#net-framework-projects)。

- 源分析与旧版分析

  本文适用于源代码分析，而适用于旧版 (二进制) 分析。 有关禁用旧版分析的信息，请参阅[如何：启用和禁用旧版代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

## <a name="net-core-and-net-standard-projects"></a>.NET Core 和 .NET Standard 项目

从 Visual Studio 2019 版本 16.3 开始，“代码分析”属性页中提供了两个复选框，可用于控制是否在生成时和设计时运行分析器。 这些选项特定于项目。

![在 Visual Studio 中启用或禁用实时代码分析或生成时的代码分析](media/run-on-build-run-live-analysis.png)

要打开该页面，右键单击“解决方案资源管理器”中的项目节点，然后选择“属性” 。 选择“代码分析”选项卡。

- 若要在生成时禁用源分析，请取消选中“在生成时运行”选项。
- 若要禁用实时源分析，请取消选中“在实时分析时运行”选项。

> [!NOTE]
> 从 Visual Studio 2019 版本 16.5 开始，如果希望使用按需代码分析执行工作流，可以在实时分析或生成期间禁用分析器执行，并按需对项目或解决方案手动触发代码分析一次。 有关手动运行代码分析的信息，请参阅[如何：手动运行托管代码的代码分析](how-to-run-code-analysis-manually-for-managed-code.md)。

## <a name="net-framework-projects"></a>.NET Framework 项目

若要关闭分析器的源代码分析，请将以下一个或多个 MSBuild 属性添加到[项目文件](../ide/solutions-and-projects-in-visual-studio.md#project-file)。

| MSBuild 属性 | 说明 | 默认 |
| - | - | - |
| `RunAnalyzersDuringBuild` | 控制分析器是否在生成时运行。 | `true` |
| `RunAnalyzersDuringLiveAnalysis` | 控制分析器是否在设计时实时分析代码。 | `true` |
| `RunAnalyzers` | 在生成时和设计时禁用分析器。 此属性优先于 `RunAnalyzersDuringBuild` 和 `RunAnalyzersDuringLiveAnalysis`。 | `true` |

示例：

```xml
<RunAnalyzersDuringBuild>false</RunAnalyzersDuringBuild>
<RunAnalyzersDuringLiveAnalysis>false</RunAnalyzersDuringLiveAnalysis>
<RunAnalyzers>false</RunAnalyzers>
```

::: moniker-end

::: moniker range="vs-2017"

## <a name="source-analysis"></a>源分析

2017 年 [1](roslyn-analyzers-overview.md) 月无法关闭Visual Studio分析。 如果要从“错误列表”中清除分析器错误，可以通过选择菜单栏上的“分析” > “运行代码分析和抑制活动问题”来抑制所有当前冲突  。 有关详细信息，请参阅[抑制冲突](use-roslyn-analyzers.md#suppress-violations)。

从 Visual Studio 2019 版本 16.3 开始，可以关闭源代码分析或按需执行它。 请考虑升级到 Visual Studio 2019。

## <a name="legacy-analysis"></a>旧版分析

可以在“代码分析”属性页上禁用旧版生成时分析。 有关详细信息，请参阅[如何：启用和禁用旧版代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

::: moniker-end

## <a name="see-also"></a>另请参阅

- [抑制冲突](use-roslyn-analyzers.md#suppress-violations)
- [如何：启用和禁用旧版代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
