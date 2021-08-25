---
title: 执行时间（“线程”视图）| Microsoft Docs
description: 查看并行可视化工具的“线程”视图中的执行时间。 执行时间由显示线程何时在逻辑内核上工作的段表示。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.execution
helpviewer_keywords:
- Concurrency Visualizer, Execution Time (Threads View)
ms.assetid: 80c100f8-2502-4613-bfef-4f4f2e09cc8d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 48455b4411994f61864a08aa05032bf8b0caafb3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122131568"
---
# <a name="execution-time-threads-view"></a>执行时间（“线程”视图）
当系统中的线程主动在逻辑内核上工作时，线程视图时间线中的这些段表示执行时间。

 通过内核上下文切换事件可检测线程状态的更改。 Windows 事件跟踪 (ETW) 每毫秒捕获一次样本堆栈。 在很短的绿色段中，则可能不会进行任何采样。 因此，某些较短的执行段可能不会显示任何调用堆栈。

 单击执行段时，并发可视化工具将显示离单击位置最近的示例堆栈。 由黑色箭头或脱字号在时间线上方显示该示例堆栈的位置，该示例堆栈显示在“当前”选项卡上。

 若要在当前视图中查看所有执行段的传统采样分析，请在可见时间线分析中单击“执行”。

## <a name="see-also"></a>另请参阅
- [执行分析报告](../profiling/execution-profile-report.md)
- [线程视图](../profiling/threads-view-parallel-performance.md)