---
title: 运行带或不带调试器的分析工具 | Microsoft Docs
description: 了解可用于分析工具的不同模式之间的差异
ms.custom: devdivchpfy22
ms.date: 01/20/2022
ms.topic: conceptual
ms.assetid: 3fcdccad-c1bd-4c67-bcec-bf33a8fb5d63
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 40ebd618891f8166d2f704401e60fc1c331e2196
ms.sourcegitcommit: f81a8f381bcdbac96d112f815737ba1df55d97a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2022
ms.locfileid: "137667442"
---
# <a name="run-profiling-tools-with-or-without-the-debugger"></a>运行带/不带调试器的分析工具

Visual Studio 提供了性能测量值和分析工具选择。 某些工具（如“CPU 使用情况”和“内存使用情况”）可以在带或不带调试器的情况下运行，也可以在发布版本或调试版本配置上运行。 [“诊断工具”窗口](../profiling/profiling-feature-tour.md#measure-performance-while-debugging)中显示的工具仅在调试会话期间运行。 [性能探查器](../profiling/profiling-feature-tour.md#post_mortem)中显示的工具在没有调试器的情况下运行，并在选择停止和收集数据后分析结果（用于事后分析）。

>[!NOTE]
>可以在 Windows 7 及更高版本中使用非调试器性能工具。 运行调试器集成分析工具需要 Windows 8 或更高版本。

非调试器性能探查器和调试器集成诊断工具提供不同的信息和体验。 调试器集成工具显示变量值并允许使用断点。 非调试器工具提供更接近最终用户体验的结果。

若要确定要使用的工具和结果，请考虑以下选项：

- 调试器集成工具与非调试器工具
  - 外部性能问题（如文件 I/O 或网络响应能力问题）在调试器或非调试器工具中看起来并没有太大差异。
  - 调试器本身会更改性能时间，因为它会执行截获异常和模块加载事件等必要的调试操作。
  - 性能探查器中的发布版本性能数字是最精准的。 调试器集成的工具结果对于与其他调试相关的度量值进行比较或使用调试器功能非常有用。
  - 有些工具（如 .NET 对象分配工具）只适用于非调试器方案。
- 调试版本与发布版本
  - 对于 CPU 密集型调用引起的问题，发布版本和调试版本之间可能存在相当大的性能差异。 检查发布版本中是否存在该问题。
  - 如果仅在调试版本期间出现此问题，则可能不需要运行非调试器工具。 对于发布生成问题，确定由调试器集成工具提供的功能是否有助于查明问题。
  - 发布版本提供的优化包括：内联函数调用和常量、修剪未使用的代码路径及以调试器无法使用的方式存储变量。 调试版本中的性能数字不太准确，因为调试版本缺乏这些优化。

## <a name="collect-profiling-data-while-debugging"></a><a name="BKMK_Quick_start__Collect_diagnostic_data"></a> 在调试期间收集分析数据

通过选择“调试” > “开始调试”或按 F5 在 Visual Studio 中开始调试时，默认情况下会出现“诊断工具”窗口。 要手动打开该窗口，请选择“调试” > “Windows” > “显示诊断工具”  。 “诊断工具”窗口显示有关事件、进程内存和 CPU 使用情况的信息。

![诊断工具窗口的屏幕截图](../profiling/media/diagnostictoolswindow.png "“诊断工具”窗口")

- 使用工具栏中的“设置”图标以选择是否要查看“内存使用情况”、“UI 分析”以及“CPU 使用情况”   。

- 在“设置”下拉列表中选择“设置”，打开“诊断工具属性页”，其中包含更多选项。

- 如果运行的是 Visual Studio Enterprise，则可以转到“工具” > “选项” > “IntelliTrace”启用或禁用 IntelliTrace。

当停止调试时，诊断会话结束。

有关详细信息，请参见:

- [通过分析 CPU 使用情况衡量应用程序性能](../profiling/beginners-guide-to-performance-profiling.md)
- [在 Visual Studio 中衡量内存使用情况](../profiling/memory-usage.md)

### <a name="the-events-tab"></a>“事件”选项卡

在调试会话期间，“诊断工具”窗口的“事件”选项卡列出了所发生的诊断事件。 使用类别前缀“断点”、“文件”及其他，可以快速扫描列表以查找类别或跳过不关心的类别。

使用“筛选器”下拉列表，以通过选择或清除特定事件类别来筛选视图内外的事件。

![诊断事件筛选器的屏幕截图](../profiling/media/diagnosticeventfilter.png "诊断事件筛选器")

使用搜索框在事件列表中查找特定字符串。 以下是搜索匹配四个事件的字符串“name”的结果：

![诊断事件搜索的屏幕截图](../profiling/media/diagnosticseventsearch.png "诊断事件搜索")

有关详细信息，请参阅 [搜索和筛选“诊断工具”窗口中的“事件”选项卡](https://devblogs.microsoft.com/devops/searching-and-filtering-the-events-tab-of-the-diagnostic-tools-window/)。

## <a name="collect-profiling-data-without-debugging"></a>在不进行调试的情况下收集分析数据

要在不进行调试的情况下收集性能数据，可以运行“性能探查器”工具。

1. 在 Visual Studio 中打开项目后，将解决方案配置设置为“发布”，然后选择“本地 Windows 调试器”（或“本地计算机”）作为部署目标。

1. 选择“调试” > “性能探查器”，或按 Alt+F2   。

1. 在诊断工具启动页上，选择一个或多个要运行的工具。 将仅显示适用于项目类型、操作系统和编程语言的工具。 选择“显示所有工具”也可查看此诊断会话禁用的工具。

   ![诊断工具的屏幕截图](../profiling/media/diaghubsummarypage.png "DIAG_SelectTool")

1. 要启动诊断会话，请选择“开始”。

   当会话正在运行时，某些工具将在 "诊断工具" 页上显示实时数据的图形，并显示用于暂停和恢复数据收集的控件。

    ![性能探查器上的数据收集屏幕截图](../profiling/media/diaghubcollectdata.png "中心收集数据")

1. 要结束诊断会话，请选择“停止收集”。

   分析的数据显示在“报表”页上。

可以保存报表，并从诊断工具启动页面上的“最近打开的会话”列表中将其打开。

![诊断工具最近打开的会话列表屏幕截图](../profiling/media/diaghubopenexistingdiagsession.png "PDHUB_OpenExistingDiagSession")

有关详细信息，请参见:

- [分析 CPU 使用情况](../profiling/cpu-usage.md)
- [分析 .NET 代码的内存使用情况](../profiling/dotnet-alloc-tool.md)
- [分析内存使用情况](../profiling/memory-usage-without-debugging2.md)
- [分析 .NET 异步代码的性能](../profiling/analyze-async.md)
- [分析数据库性能](../profiling/analyze-database.md)
- [分析 GPU 使用情况](../profiling/gpu-usage.md)

## <a name="collect-profiling-data-from-the-command-line"></a>通过命令行收集分析数据

若要从命令行测量性能数据，可以使用 Visual Studio 或远程工具随附的 VSDiagnostics.exe。 这适用于在未安装 Visual Studio 的系统上捕获性能跟踪，或用于编写性能跟踪集合的脚本。 有关详细说明，请参阅[从命令行测量应用程序性能](../profiling/profile-apps-from-command-line.md)。