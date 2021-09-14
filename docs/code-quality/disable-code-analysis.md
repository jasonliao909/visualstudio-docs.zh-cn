---
title: 关闭代码分析
ms.date: 09/01/2020
description: 了解如何在 .NET .NET Standard Core、Visual Studio和 .NET Framework 项目中关闭.NET Framework分析。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601331"
---
# <a name="disable-source-code-analysis-for-net"></a>禁用 .NET 的源代码分析

::: moniker range=">=vs-2019"

此页面可帮助你禁用代码中的代码Visual Studio。 可以禁用哪些功能存在限制，关闭代码分析的过程因几个因素而不同：

- Project类型 (.NET Core/Standard 与 .NET Framework) 

  .NET Core 和 .NET Standard 项目在 Code Analysis 属性页上具有选项，通过这些选项可以关闭作为 NuGet 包安装的分析器的代码分析。 有关详细信息，请参阅 [.NET Core 和 .NET Standard项目](#net-core-and-net-standard-projects)。 若要为项目关闭源代码.NET Framework，请参阅.NET Framework[项目](#net-framework-projects)。

- 源分析与旧分析

  本主题适用于源代码分析，而适用于旧版 (二进制) 分析。 有关禁用旧分析的信息，请参阅 [如何：启用和禁用旧代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

## <a name="net-core-and-net-standard-projects"></a>.NET Core 和 .NET Standard 项目

从 Visual Studio 2019 版本 16.3 开始，Code Analysis 属性页中提供了两个复选框，可用于控制分析器是否在生成时和设计时运行。 这些选项特定于项目。

![启用或禁用实时代码分析或生成Visual Studio](media/run-on-build-run-live-analysis.png)

若要打开此页，请右键单击"属性"中的解决方案资源管理器并选择 **"** 属性 **"。** 选择 **"Code Analysis** 选项卡。

- 若要在生成时禁用源分析，请取消选中" **生成时运行"** 选项。
- 若要禁用实时源分析，请取消选中" **实时运行分析"** 选项。

> [!NOTE]
> 从 Visual Studio 2019 版本 16.5 开始，如果你更喜欢按需代码分析执行工作流，可以在实时分析和/或按需生成和手动触发代码分析一次期间禁用分析器执行。 有关手动运行代码分析的信息，请参阅[如何：为托管Code Analysis手动运行代码](how-to-run-code-analysis-manually-for-managed-code.md)。

## <a name="net-framework-projects"></a>.NET Framework 项目

若要关闭分析器源代码分析，将以下一个或多个MSBuild属性添加到[项目文件](../ide/solutions-and-projects-in-visual-studio.md#project-file)。

| MSBuild 属性 | 说明 | 默认 |
| - | - | - |
| `RunAnalyzersDuringBuild` | 控制分析器是否在生成时运行。 | `true` |
| `RunAnalyzersDuringLiveAnalysis` | 控制分析器在设计时是否实时分析代码。 | `true` |
| `RunAnalyzers` | 在生成和设计时禁用分析器。 此属性优先于 和 `RunAnalyzersDuringBuild` `RunAnalyzersDuringLiveAnalysis` 。 | `true` |

示例：

```xml
<RunAnalyzersDuringBuild>false</RunAnalyzersDuringBuild>
<RunAnalyzersDuringLiveAnalysis>false</RunAnalyzersDuringLiveAnalysis>
<RunAnalyzers>false</RunAnalyzers>
```

::: moniker-end

::: moniker range="vs-2017"

## <a name="source-analysis"></a>源分析

无法在 2017[年 1](roslyn-analyzers-overview.md)月Visual Studio源分析。 如果要从"错误列表"中清除分析器错误，可以通过在菜单栏上选择"分析运行Code Analysis"取消活动问题"来禁止显示所有  >  当前冲突。 有关详细信息，请参阅[抑制冲突](use-roslyn-analyzers.md#suppress-violations)。

从 Visual Studio 2019 版本 16.3 开始，可以关闭源代码分析或按需执行。 请考虑升级到 2019 Visual Studio 2019。

## <a name="legacy-analysis"></a>旧版分析

可以在"属性"页上禁用旧的生成 **Code Analysis** 分析。 有关详细信息，请参阅 [如何：启用和禁用旧代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

::: moniker-end

## <a name="see-also"></a>另请参阅

- [禁止显示冲突](use-roslyn-analyzers.md#suppress-violations)
- [如何：启用和禁用旧代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
