---
title: 调试多线程应用程序 | Microsoft Docs
description: 在 Visual Studio 中调试多线程应用程序。 查看有关调试多线程应用的工具和其他文章。
ms.date: 11/06/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.gputthreads
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- debugging [Visual Studio], high-performance computing
- debugging [Visual Studio], multithreaded
- multithreaded debugging
- high-performance debugging
ms.assetid: 9d175bc2-1d95-4c47-9bc3-9755af968a9c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 70559b55eee8d4c521ec6bc31e16893e89ef3b3c
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129973163"
---
# <a name="debug-multithreaded-applications-in-visual-studio"></a>在 Visual Studio 中调试多线程应用程序
线程是操作系统向其授予处理器时间的指令序列。 在操作系统中运行的每个进程都包含至少一个线程。 包含多个线程的进程称为多线程。

具有多个处理器、多核处理器或超线程进程的计算机可以同时运行多个线程。 使用许多线程并行处理可以极大地提高程序性能，但是，由于会跟踪许多线程，也使得调试更加困难。

多线程处理可能会引入新类型的潜在 bug。 例如，两个或更多线程可能需要访问同一资源，但是一次只能有一个线程可以安全地访问该资源。 必须使用某种形式的互斥以确保任何时候都仅有一个线程访问资源。 如果互斥未正确实现，则可能形成死锁条件，这种条件下，任何线程都不会执行。 对于调试而言，死锁通常是难以解决的问题。

## <a name="tools-for-debugging-multithreaded-apps"></a>用于调试多线程应用的工具

Visual Studio 提供不同的工具用于调试多线程应用程序。

- 对于线程，用于调试线程的主要工具有“线程”窗口、源窗口中的线程标记、“并行堆栈”窗口、“并行监视”窗口和“调试位置”工具栏   。 若要了解“线程”窗口和“调试位置”工具栏，请参阅[演练：使用“线程”窗口进行调试](../debugger/how-to-use-the-threads-window.md)。 若要了解如何使用“并行堆栈”和“并行监视”窗口，请参阅[开始调试多线程应用程序](../debugger/get-started-debugging-multithreaded-apps.md)。 这两个主题演示如何使用线程标记。

- 对于使用[任务并行库 (TPL)](/dotnet/standard/parallel-programming/task-parallel-library-tpl) 或[并发运行时](/cpp/parallel/concrt/concurrency-runtime/)的代码，调试的主要工具是“并行堆栈”窗口、“并行监视”窗口和“任务”窗口（该窗口也支持 JavaScript）。 若要开始使用，请参阅[演练：调试并行应用程序](../debugger/walkthrough-debugging-a-parallel-application.md)和[演练：调试 C++ AMP 应用程序](/cpp/parallel/amp/walkthrough-debugging-a-cpp-amp-application)。

- 对于调试 GPU 上的线程，主要工具是“GPU 线程”窗口。 请参阅[如何：使用 GPU 线程窗口](../debugger/how-to-use-the-gpu-threads-window.md)。

- 对于进程，主要工具是“附加到进程”对话框、“进程”窗口和“调试位置”工具栏。

Visual Studio 还提供了功能强大的断点和跟踪点，在调试多线程应用程序时，它们十分有用。 使用断点条件和筛选器可将断点置于单个线程上。 使用跟踪点可以在不中断的情况下跟踪程序的执行，以研究诸如死锁之类的问题。 有关详细信息，请参阅[断点操作和跟踪点](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints)。

调试具有用户界面的多线程应用程序可能会特别困难。 可以考虑在另一台计算机上运行应用程序并使用远程调试。 有关详细信息，请参阅[远程调试](../debugger/remote-debugging.md)。

## <a name="articles-about-debugging-multithreaded-apps"></a>有关调试多线程应用的文章

 [开始调试多线程应用程序](../debugger/get-started-debugging-multithreaded-apps.md)

有关线程调试功能的教程，重点介绍“并行堆栈”窗口和“并行监视”窗口中的功能。

 [用于调试线程和进程的工具](../debugger/debug-threads-and-processes.md)

列出用于调试线程和进程的工具的功能。

 [调试多个进程](../debugger/debug-multiple-processes.md)

说明如何调试多个进程。

 [演练：使用“线程”窗口进行调试](../debugger/how-to-use-the-threads-window.md)。

演示如何使用“线程”窗口和“调试位置”工具栏的演练。

 [演练：调试并行应用程序](../debugger/walkthrough-debugging-a-parallel-application.md)

演示如何使用“并行堆栈”和“任务”窗口的演练。

 [如何：在调试时切换到另一个线程](../debugger/how-to-switch-to-another-thread-while-debugging.md)

将调试上下文切换到其他线程的几种方法。

 [如何：标记线程和取消标记线程](../debugger/how-to-flag-and-unflag-threads.md)

在调试过程中，标记要格外关注的线程，或为其设置标志。

 [如何：在高性能群集上进行调试](../debugger/how-to-debug-on-a-high-performance-cluster.md)

对运行于高性能群集上的应用程序进行调试的技术。

 [调试本机代码中的线程时的提示](../debugger/tips-for-debugging-threads-in-native-code.md)

对于调试本机线程十分有用的简单技术。

 [如何：在本机代码中设置线程名称](../debugger/how-to-set-a-thread-name-in-native-code.md)

为在“线程”窗口中查看的线程提供一个名称。

 [如何：在托管代码中设置线程名称](../debugger/how-to-set-a-thread-name-in-managed-code.md)

为在“线程”窗口中查看的线程提供一个名称。

## <a name="see-also"></a>请参阅

- [使用断点](../debugger/using-breakpoints.md)
- [线程处理](/dotnet/standard/threading/index)
- [组件中的多线程处理](/previous-versions/3es4b6yy(v=vs.140))
- [针对旧代码的多线程处理支持](/cpp/parallel/multithreading-support-for-older-code-visual-cpp)
- [调试线程和进程](../debugger/debug-threads-and-processes.md)
- [远程调试](../debugger/remote-debugging.md)