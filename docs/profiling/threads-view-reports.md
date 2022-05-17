---
title: 并发可视化工具中的线程视图报表 | Microsoft Docs
description: 了解在线程视图中，你可以使用报表确定哪些线程在执行段期间执行代码。
ms.date: 05/06/2022
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.report.blocking
- vs.cv.threads.report.diskoperations
- vs.cv.threads.report.execution
- vs.cv.threads.report.markers
- vs.cv.threads.report.executionbreakdown
helpviewer_keywords:
- Concurrency Visualizer, Threads View Reports (Parallel Performance)
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 74bcf41a2ea3a19f088f5c5c42f5f04afda9f5df
ms.sourcegitcommit: caf5ca17efde4dc4de8b1bdfbe7770f6d705024d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2022
ms.locfileid: "145018125"
---
# <a name="threads-view-reports-in-the-concurrency-visualizer"></a>并发可视化工具中的线程视图报表

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

 本文提供有关并发可视化工具线程视图中的报表的信息。

## <a name="blocking-time-profile-report"></a>阻塞时间分析报告

分析报告提供特定于每个阻塞类别（例如，“I/O”或“同步”）的调用堆栈的合计阻塞时间数据。 优先报告列出抢占当前进程的进程以及抢占实例数。 为了生成阻塞分析报告，工具会收集阻塞 API 调用并将它们累计到调用堆栈树中。 这些报告中显示的数据因当前时间范围、隐藏线程和以下两个可能应用的筛选器而异：

- 如果选择“仅我的代码”，则仅会显示具有用户代码的堆栈帧和该用户代码下的一个级别。

- 如果设置了降噪值，则将跳过低于指定频率的排序堆栈。

  展开所有调用树项，找到消耗阻塞时间的代码行。 若要找到某一项的源行，请在其快捷菜单上选择“查看源”。 若要找到调用此项的代码行，请在快捷菜单上选择“查看调用站点”。 如果只有一个调用站点可用，则此命令将连接到该调用站点的突出显示代码行。 如果有多个调用站点可用，则此命令将打开一个对话框，可选择其中一项，然后选择“转到源”按钮以找到突出显示的调用站点。 在查看具有最多实例和/或最大时间的调用站点的源代码时，这往往最为有用。

### <a name="blocking-time-report-columns"></a>阻塞时间报告列
 下表显示每个阻塞时间报表的列。

|列名称|说明|
|-----------------|-----------------|
|**名称**|调用堆栈每个级别的函数的名称。|
|**实例**|可见时间段内阻塞调用的实例数。|
|**非独占阻塞时间**|在上滚到此调用堆栈树级别的所有堆栈上所花费的总阻塞时间。 非独占数是此函数的独占阻塞时间及其所有子节点的独占阻塞时间的总和。|
|**独占阻塞时间**|此函数处于最低调用堆栈级别期间所花费的总阻塞时间。 具有较高独占阻塞时间的唯一调用堆栈项可能是相关的函数。|
|**API/Wait 类别**|仅对处于最低调用堆栈级别的函数显示。 如识别阻塞调用的签名，则将提供阻塞 API 的名称。 如果未识别签名，则提供内核所报告的信息。|
|**详细信息**|该函数的完全限定名。 这包括行计数（如果有）。|

#### <a name="synchronization"></a>同步
 同步报表显示对在同步上进行阻止的片段的调用，以及每个调用堆栈的合计阻塞时间。 有关详细信息，请参阅[同步时间](../profiling/threads-view-timeline-reports.md#synchronization-time)。

#### <a name="sleep"></a>睡眠状态
 休眠报表显示对分配给休眠时间的阻塞时间的调用，以及每个调用堆栈的合计阻塞时间。 有关详细信息，请参阅[睡眠时间](../profiling/threads-view-timeline-reports.md#sleep-time)。

#### <a name="io"></a>I/O
 I/O 报表显示对在 I/O 上进行阻止的片段的调用，以及每个调用堆栈的合计阻塞时间。 有关详细信息，请参阅 [I/O 时间（线程视图）](../profiling/threads-view-timeline-reports.md#io-time-threads-view)。

#### <a name="memory-management"></a>内存管理
 内存管理报表显示对在内存管理操作上进行阻止的片段的调用，以及每个调用堆栈的合计阻塞时间。 有关详细信息，请参阅[内存管理时间](../profiling/threads-view-timeline-reports.md#memory-management-time)。

#### <a name="preemption"></a>优先
 优先报告列出抢占当前进程的进程以及实例数。  您可以展开每个进程，查看当前进程中被替换的线程，以及按线程查看抢占实例的明细。 此阻塞报告的可操作性弱于其他报告，因为抢占通常是由操作系统施加于进程的，而不是由代码中的问题而施加。 有关详细信息，请参阅[抢占时间](../profiling/threads-view-timeline-reports.md#preemption-time)。

#### <a name="ui-processing"></a>UI 处理
 UI 处理报表显示对在 UI 处理块上进行阻止的片段的调用，以及每个调用堆栈的合计阻塞时间。 有关详细信息，请参阅 [UI 处理时间](../profiling/threads-view-timeline-reports.md#ui-processing-time)。

## <a name="disk-operations-report-threads-view"></a>磁盘操作报告（线程视图）

磁盘操作报告显示磁盘通道中的磁盘 I/O 操作。

 对于代表正在当前可见时间窗口中进行分析的进程而发生的每次磁盘访问，将报告以下信息：

- 执行磁盘访问的进程的名称和 PID

- 访问磁盘的线程的 ID

- 被访问的文件的名称。

- 每个文件的读取数

- 读取的字节数

- 读取延迟时间（以毫秒为单位）

- 写入数

- 写入的字节数

- 写入延迟时间（以毫秒为单位）

## <a name="execution-profile-report"></a>执行分析报告

执行分析报告是传统的采样分析。 线程在逻辑内核上运行期间内，将大约每毫秒进行一次采样，并且并发可视化工具可通过调用累积的堆栈集构建典型的调用关系树。 此表中的数据可能受到当前时间范围、隐藏线程和可能应用的筛选器的影响：

- 如果选择“仅我的代码”，则仅会显示具有用户代码的堆栈帧和该用户代码下的一个级别。

- 如果设置了降噪值，则将把低于指定频率的排序堆栈筛从报告中筛选出去

  下表显示报告中的列。

|列|说明|
|------------|-----------------|
|名称|调用堆栈每个级别的函数的名称。|
|非独占样本数|为汇总到此调用堆栈树级别的所有堆栈收集的样本总数。 非独占数是此函数的独占样本数和所有子节点的非独占计数器的总和。|
|独占样本|收集的样本总数，其中此函数是最低的调用堆栈。|
|非独占百分比|非独占样本列中显示的总样本百分比。 百分比舍入到两个小数位。|
|独占百分比|独占样本列中显示的总样本百分比。 百分比舍入到两个小数位。|
|详细信息|该函数的完全限定名。 这包括行计数（如果有）。|

 可在[执行时间（“线程”视图）](../profiling/threads-view-timeline-reports.md#execution-time-threads-view)视图中查看此报告表格。

## <a name="markers-report"></a>标记报告

标记报告列出所显示时间范围内的标记。  平移、缩放或隐藏通道，可能会导致标记显示或消失。 报告中包含有关各个标记的以下信息：

- 开始时间，相对于跟踪的开始时间。

- 持续时间。 标志和消息代表瞬时，因此它们的持续时间为零。

- 生成标记的线程的 ID。

- 生成标记的 Windows 事件跟踪 (ETW) 提供程序。

- 从中写入标记的标记序列。

- 标记所属的事件类别。

- 标记的重要性级别。

- 标记的类型（范围、标志或消息）。

- 有关标记所代表的内容的简略说明。

  选择“导出”按钮，将标记报告保存为 CSV 文件。 可以将 CSV 文件中的数据与其他应用或工具一起使用。

> [!NOTE]
> 标记报告可显示 1,000 个标记。 若要查看全部标记，请将整个报告导出到 CSV 文件。

## <a name="per-thread-summary-report"></a>“每线程摘要”报告

此条形图显示在当前可见时间范围内，各活动类别中的每个非隐藏线程所花费的时间比例。 “执行”表示线程正在执行；所有其他类别表示线程正在进行等待。

## <a name="see-also"></a>另请参阅

- [并发可视化工具](../profiling/concurrency-visualizer.md)
