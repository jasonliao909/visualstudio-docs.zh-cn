---
title: 并发可视化工具中的线程视图时间线报表 | Microsoft Docs
description: 了解在线程视图中，你可以使用时间线报表确定哪些线程在执行段期间执行代码。
ms.date: 05/06/2022
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.execution
- vs.cv.threads.timeline.io
- vs.cv.threads.timeline.paging
- vs.cv.threads.timeline.preemption
- vs.cv.threads.timeline.sleep
- vs.cv.threads.timeline.synchronization
- vs.cv.threads.timeline.uiprocessing
helpviewer_keywords:
- Concurrency Visualizer, Threads View Timeline Reports (Parallel Performance)
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: dd77d5f695549d9d9618bde9a888959469feeb6b
ms.sourcegitcommit: caf5ca17efde4dc4de8b1bdfbe7770f6d705024d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2022
ms.locfileid: "145018124"
---
# <a name="threads-view-timeline-reports-in-the-concurrency-visualizer"></a>并发可视化工具中的线程视图时间线报表

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

 本文提供有关并发可视化工具线程视图中的时间线报表的信息。

## <a name="execution-time-threads-view"></a>执行时间（“线程”视图）

当系统中的线程主动在逻辑内核上工作时，线程视图时间线中的这些段表示执行时间。

 通过内核上下文切换事件可检测线程状态的更改。 Windows 事件跟踪 (ETW) 每毫秒捕获一次样本堆栈。 在很短的绿色段中，则可能不会进行任何采样。 因此，某些较短的执行段可能不会显示任何调用堆栈。

 单击执行段时，并发可视化工具将显示离单击位置最近的示例堆栈。 由黑色箭头或脱字号在时间线上方显示该示例堆栈的位置，该示例堆栈显示在“当前”选项卡上。

 若要在当前视图中查看所有执行段的传统采样分析，请在可见时间线分析中单击“执行”。

## <a name="io-time-threads-view"></a>I/O 时间（“线程”视图）

时间线中的这些段与归类为 I/O 的阻塞时间关联。 这意味着一个线程正在等待 I/O 操作完成。 此线程可能已在 API 中被阻止，或由将并发可视化工具视为 I/O 的 I/O 相关内核等待阻止。 此组中包括 `CreateFile()`、`ReadFile()` 和 `WSARecv()` 等 API。

## <a name="memory-management-time"></a>内存管理时间

时间线中的这些段与归类为内存管理的阻塞时间关联。 此方案意味着线程被与内存管理操作（如分页）关联的事件所阻止。 在此时间内，线程被阻止在并发可视化工具视为内存管理的 API 或内核状态下。 这些包括诸如分页和内存分配这类事件。

 检查关联的调用堆栈和分析报告，以便更好地了解归类为内存管理的阻塞的基本原因。

## <a name="preemption-time"></a>抢占时间

时间线中的这些段与归类为“抢占”的阻塞时间关联。 此类别表示由于以下原因之一断开线程：

- 计划程序使用更高优先级的线程将其替换。

- 线程的执行量程过期，且其他线程已作好执行准备。

  在此时间内，由于并发可视化工具被视为“抢占”这一内核等待原因，已阻止线程。 当线程被排出逻辑核心时，抢占段开始；当线程继续执行时，抢占段结束。

  抢占段的工具提示会显示导致抢占的进程或线程的名称。 然而，这并不表示接管的进程或线程在抢占期间内会实际运行。

## <a name="sleep-time"></a>睡眠时间

时间线中的这些时间段与归类为睡眠的阻塞时间关联。 睡眠类别意味着某线程自动放弃其逻辑内核并且不执行任何工作。 在此时间内，线程已在被并发可视化工具计数为睡眠的 API 中阻塞。 `Sleep()` 和 `SwitchToThread()` 等 API 就归为此组。

## <a name="synchronization-time"></a>同步时间

时间线中的这些段与归类为同步的阻止时间关联。 当线程被标记为在同步中阻止时，表示出现了下列情况之一：

- 执行该线程可能会导致调用已知线程同步 API（如 `EnterCriticalSection()` 或 `WaitForSingleObject()`）。

- API 匹配算法无法做到非常全面，因此一些可映射到其他类别的 API 也可能显示为同步，这是因为调用堆栈中的帧会最终到达映射到此类别的基础内核阻止基元。

  若要了解线程阻止事件的基本原因，可仔细检查阻止调用堆栈和分析报告。

## <a name="ui-processing-time"></a>UI 处理时间

时间线中的这些时间段与归类为 UI 处理的阻塞时间关联。 这表示有一个线程正在发送 Windows 消息或正在执行其他用户界面 (UI) 操作。 在此时间内，线程已在被并发可视化工具计数为 UI 处理的 API 中阻塞。 `GetMessage()` 和 `MsgWaitForMultipleObjects()` 等 API 就归为此组。

 如果未标识预定义的阻塞 API，请检查调用堆栈和分析报告，确定造成延迟的根本原因。

 UI 处理类别帮助你理解 GUI 应用程序的响应能力，非常适合依赖 UI 响应能力的应用程序。 例如，如果应用程序中的 UI 线程能够将 100% 的时间用于 UI 处理，则该应用程序的响应速度可能会很快。 但是，如果 UI 线程花费了大量时间在其他类别上，则需查找根本原因并考虑降低该线程上的非 UI 类别。

## <a name="see-also"></a>另请参阅

- [并发可视化工具](../profiling/concurrency-visualizer.md)
