---
title: 使用“任务”窗口 | Microsoft Docs
description: 任务是可并发运行的异步操作。 多个任务可以在同一线程上运行。 使用“任务”查看任务和 WinJS.Promise 对象信息。
ms.custom: SEO-VS-2020
ms.date: 03/18/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.paralleltasks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, parallel tasks window
ms.assetid: bd5e0612-a0dc-41cf-a7af-1e87d0d5c35f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: f4a804c88f48274f67debee492c3452fa4086004
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122030485"
---
# <a name="using-the-tasks-window-c-visual-basic-c"></a>使用“任务”窗口（C#、Visual Basic、C++）

“任务”窗口与“线程”窗口类似，但它显示的是有关 <xref:System.Threading.Tasks.Task?displayProperty=fullName>、[task_handle](/cpp/parallel/concrt/reference/task-group-class) 或 [WinJS.Promise](/previous-versions/windows/apps/br211867(v=win.10)) 对象（而不是各个线程）的信息。 与线程一样，任务表示可并行运行的异步操作；但是，多个任务可以在同一个线程上运行。

在托管代码中，当使用 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 对象或 await 和 async 关键字（在 Visual Basic 中为 Await 和 Async）时，可使用“任务”窗口。 有关托管代码中的任务的详细信息，请参阅[并行编程](/dotnet/standard/parallel-programming/index)。

在本机代码中，当使用[任务组](/cpp/parallel/concrt/task-parallelism-concurrency-runtime)、[并行算法](/cpp/parallel/concrt/parallel-algorithms)、[异步代理](/cpp/parallel/concrt/asynchronous-agents)和[轻量级任务](/cpp/parallel/concrt/task-scheduler-concurrency-runtime)时，可使用“任务”窗口。 有关本机代码中的任务的详细信息，请参阅[并发运行时](/cpp/parallel/concrt/concurrency-runtime)。

在 JavaScript 中，当使用 promise `.then` 代码时，可使用“任务”窗口。 有关详细信息，请参阅 [JavaScript 中的异步编程（UWP 应用）](/previous-versions/windows/apps/hh700330(v=win.10))。

每次中断调试器时都可以使用“任务”窗口。 通过单击“窗口”，然后单击“任务”，可以在“调试”菜单上访问该窗口。 下图显示了处于默认模式的“任务”窗口。

![“任务”窗口](../debugger/media/parallel_tasks_window.png "Parallel_Tasks_Window")

> [!NOTE]
> 在托管代码中，当托管线程处于休眠或联接状态时，状态为 [TaskStatus.Created](<xref:System.Threading.Tasks.TaskStatus.Created>)、[TaskStatus.WaitingForActivation](<xref:System.Threading.Tasks.TaskStatus.WaitingForActivation>) 或 [TaskStatus.WaitingToRun](<xref:System.Threading.Tasks.TaskStatus.WaitingToRun>) 的 <xref:System.Threading.Tasks.Task> 可能不会在“任务”窗口中显示。

## <a name="tasks-column-information"></a>任务列信息

“任务”窗口中的列显示了以下信息。

|列名|描述|
|-----------------|-----------------|
|**标记**|显示哪些任务已被标记，并且你可以标记或取消标记任务。|
|**图标**|黄色箭头指示当前任务。 当前任务是当前线程上处于最顶层的任务。<br /><br /> 白色箭头指示中断的任务，即调用调试器时的任务。<br /><br /> 暂停图标指示已被用户冻结的任务。 在列表中右击某一任务可以冻结或取消冻结该任务。|
|**ID**|系统为任务提供的编号。 在本机代码中，该编号是任务的地址。|
|**状态**|任务的当前状态（已计划、活动、已阻止、已死锁、正在等待或已完成）。 已计划的任务是指尚未运行的任务，因此它没有调用堆栈、已分配的线程或相关信息。<br /><br /> 活动任务是指在中断调试器之前正在执行代码的任务。<br /><br /> 正在等待或已阻止的任务是指因以下原因而被阻止的任务：正在等待向事件发送信号、释放锁或完成其他任务。<br /><br /> 死锁任务是指其线程与其他线程相互死锁的正在等待的任务。<br /><br /> 将鼠标悬停在已死锁或正在等待的任务的“状态”单元格上，详细了解阻止原因。 **警告：** “任务”窗口只针对使用 Wait Chain Traversal (WCT) 所支持的同步基元的受阻任务报告死锁。 例如，对于某个使用 WCT 的 <xref:System.Threading.Tasks.Task> 死锁对象，调试器会报告“正在等待-已死锁”。 对于由并发运行时管理、不使用 WCT 的死锁任务，调试器则会报告“正在等待”。 有关 WCT 的详细信息，请参阅 [Wait Chain Traversal](/windows/desktop/Debug/wait-chain-traversal)。|
|**开始时间**|任务变为活动状态的时间。|
|**持续时间**|任务已处于活动状态的秒数。|
|**完成时间**|任务完成的时间。|
|**位置**|任务调用堆栈中的当前位置。 将鼠标指针悬停在此单元格上可以查看任务的整个调用堆栈。 已计划的任务在该列中没有相应的值。|
|**Task**|创建任务时传递到该任务的初始方法以及任何参数。|
|**AsyncState**|对于托管代码，即任务状态。 默认情况下，此列被隐藏。 若要显示此列，请打开其中一个列标题的上下文菜单。 选择“列”，再选择“AsyncState”。|
|**父级**|创建此任务的任务的 ID。 如果为空白，则说明该任务没有父级。 这仅适用于托管程序。|
|**线程分配**|运行任务的线程的 ID 和名称。|
|**AppDomain**|对于托管代码，该列表示要在其中执行任务的应用程序域。|
|**task_group**|对于本机代码，该列表示计划任务的 [task_group](/cpp/parallel/concrt/reference/task-group-class) 对象的地址。 对于异步代理和轻量级任务，该列设置为 0。|
|**Process**|运行任务的进程的 ID。|

 通过右击列标题并选择所需的列可以向视图添加列。 （通过清除所选内容即可删除列。）你还可以通过向左或向右拖动列来对列重新排序。 列的快捷菜单如下图所示。

 ![“任务”窗口中的“快捷视图”菜单](../debugger/media/parallel_tasks_contextmenu.png "Parallel_Tasks_ContextMenu")

## <a name="sorting-tasks"></a>对任务进行排序
 若要按列条件对任务进行排序，请单击相应的列标题。 例如，通过单击“ID”列标题，可以按任务 ID 对任务进行排序：1、2、3、4、5 等等。 若要反转排序顺序，请再次单击相应的列标题。 当前排序列和排序顺序由该列上的箭头指示。

## <a name="grouping-tasks"></a>对任务进行分组
 你可以根据列表视图中的任何列对任务进行分组。 例如，通过右击“状态”列标题并单击“按 > [状态]分组” ，可以将所有具有相同状态的任务划分为一个组。 例如，你可以快速查看正在等待的任务，以便关注其被阻止的原因。 您还可以在调试会话期间折叠不相关的组。 同样，还可以按其他列进行分组。 只需单击组标题旁的按钮即可标记或取消标记组。 下图显示了处于分组模式下的“任务”窗口。

 ![“任务”窗口中的分组模式](../debugger/media/parallel_tasks_groupedmode.png "Parallel_Tasks_GroupedMode")

## <a name="parent-child-view"></a>父子视图
 （此视图仅可用于托管代码。）通过右键单击“状态”列标题，然后单击“分组依据” > “父视图”，你可以将任务列表更改为分层视图；在分层视图中，每个子任务都是一个子节点，可以在其父级下显示或隐藏该子节点  。

## <a name="flagging-tasks"></a>标记任务
 可以标记运行任务的线程，方法是选择任务列表项，然后从上下文菜单中选择“标记分配的线程”，或者单击第一列中的旗形图标。 如果标记了多个任务，则可以按标记列进行排序以在顶部显示标记的所有任务，从而仅关注这些任务。 此外，还可以使用“并行堆栈”窗口仅查看已标记任务。 这样，你便可以为调试操作滤出不相关的任务。 标记不会在调试会话之间保留。

## <a name="freezing-and-thawing-tasks"></a>冻结和解冻任务
 通过右击任务列表项并单击“冻结指定的线程”，可以冻结运行任务的线程。 （如果任务已冻结，该命令则为“解冻指定的线程”。）如果已冻结线程，则逐句通过当前断点后的代码时，将不会执行该线程。 “冻结此线程之外的所有线程”命令冻结除正在执行任务列表项的线程以外的所有线程。

 下图所示为每项任务的其他菜单项。

 ![“任务”窗口中的“快捷线程”菜单](../debugger/media/parallel_tasks_contextmenu2.png "Parallel_Tasks_ContextMenu2")

## <a name="switching-the-active-task-or-frame"></a>切换活动任务或帧

“切换到任务”命令使当前任务成为活动任务。 “切换到帧”命令使所选堆栈帧成为活动堆栈帧。 调试器上下文切换到当前任务或所选堆栈帧。

## <a name="see-also"></a>请参阅

- [初探调试器](../debugger/debugger-feature-tour.md)
- [调试托管代码](../debugger/debugging-managed-code.md)
- [并行编程](/dotnet/standard/parallel-programming/index)
- [并发运行时](/cpp/parallel/concrt/concurrency-runtime)
- [使用“并行堆栈”窗口](../debugger/using-the-parallel-stacks-window.md)
- [演练：调试并行应用程序](../debugger/walkthrough-debugging-a-parallel-application.md)