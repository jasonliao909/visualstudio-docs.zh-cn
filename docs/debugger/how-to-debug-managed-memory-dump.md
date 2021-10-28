---
title: 使用 .NET 诊断分析器来调试托管内存转储 | Microsoft Docs
description: 了解如何使用 Visual Studio 的 .NET 诊断分析器来分析托管内存转储
ms.custom: SEO-VS-2021
ms.date: 04/21/2021
ms.topic: how-to
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- analyzers
- dump debugging
- debugging managed memory dump
- debugging [Visual Studio]
author: poppastring
ms.author: madownie
manager: andster
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: 083095ad534aa6b9131ba103178313cb1cdc4b7c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641990"
---
# <a name="how-to-debug-a-managed-memory-dump-with-net-diagnostic-analyzers"></a>如何使用 .NET 诊断分析器来调试托管内存转储



在本教程中，将：

> [!div class="checklist"]
> * 打开内存转储
> * 选择并对转储执行分析器
> * 审阅分析器结果
> * 转到有问题的代码


在本文所述的示例中，存在的问题是，你的应用没有及时响应请求。 


## <a name="opening-a-memory-dump-in-visual-studio"></a>在 Visual Studio 中打开内存转储

1. 在 Visual Studio 中，使用“文件”>“打开”>“文件”菜单命令来打开内存转储，然后选择内存转储。

1. 注意到，在“内存转储摘要”页上，有一个名为“运行诊断分析”的新“操作”。

   ![操作 - 诊断分析](../debugger/media/diagnostic-analyzer-dump-summary-actions.png)

1. 选择此操作，以启动调试器，并打开新的“诊断分析”页，其中列出了按基础症状组织的可用分析器选项。


## <a name="select-and-execute-analyzers-against-the-dump"></a>选择并对转储执行分析器

若要调查这些症状，可以在“进程响应性”下找到最佳选项，因为它与本示例中的问题最匹配。

   ![选择诊断分析器](../debugger/media/diagnostic-analyzer-diagnostics-analysis-window.png)

1. 单击“分析”按钮，以启动调查过程 

1. 分析器将根据在内存转储中捕获的进程信息和 CLR 数据的组合来显示结果。
 
## <a name="review-the-results-of-the-analyzers"></a>审阅分析器结果

1. 在此示例中，分析器发现了两个错误。 选择分析器结果来查看“分析摘要”和建议的“修正”。

   ![诊断分析器结果](../debugger/media/diagnostic-analyzer-diagnostics-analysis-results.png)

1. “分析摘要”指明“CLR 线程池的线程极其缺乏”。 此信息表明，CLR 目前已经使用了所有可用的线程池线程；也就是说，在线程被释放之前，你的服务无法响应任何新请求。

    > [!NOTE] 
    > 在此示例中，“修正”指明“不要同步地等待监视器、事件、任务或其他任何可能阻止线程的对象。 看看能否将方法更新为异步的。”

## <a name="navigating-to-the-problematic-code"></a>转到有问题的代码

下一个作业是查找有问题的代码。

1. 在你单击“显示调用堆栈”链接后，Visual Studio 会立即切换到出现此行为的线程。

1. “调用堆栈”窗口会显示一些方法，这些方法可能可以快速区分我的代码 (SyncOverAsyncExmple. *) 与 Framework 代码 (System.* )。

   ![诊断分析器链接到调用堆栈](../debugger/media/diagnostic-analyzer-call-stack.png)

1. 每个调用堆栈帧都对应于一个方法，在你双击堆栈帧后，Visual Studio 会转到此线程上直接导致这种情况发生的代码。

1. 在此示例中，没有任何符号或代码，但在“未加载符号”页上，可以选择[“反向编译源代码”](../debugger/decompilation.md)选项。

   ![反向编译](../debugger/media/diagnostic-analyzer-decompilation.png)

1. 在下面的反向编译源代码中，可以明显地看到一个异步任务 (ConsumeThreadPoolThread) 正在调用同步阻塞性函数。

    > [!NOTE]  
    > “DoSomething()”方法包含 WaitHandle.WaitOne 方法，此方法阻塞当前线程池线程，直到它收到信号。

   为了提升应用响应性，请务必从所有异步上下文中删除阻塞性同步代码。

   ![分析反向编译代码](../debugger/media/diagnostic-analyzer-decompiled-code.png)


## <a name="see-also"></a>另请参阅

* [在调试器中使用转储文件](../debugger/using-dump-files.md)
* [在调试时从 .NET 程序集生成源代码](../debugger/decompilation.md)
* [指定符号 (.pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
