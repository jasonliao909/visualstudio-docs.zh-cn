---
title: 选择内存分析工具
description: 了解可用于查找内存泄露和内存低效使用情况的工具，例如内存使用情况工具和 .NET 对象分配工具。
ms.date: 02/18/2022
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 236468571e26a31a0eed5c0197ebea0bdf408620
ms.sourcegitcommit: 2a3dc3ea8584c0e500c87c2c367a4719455b8dee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2022
ms.locfileid: "139129073"
---
# <a name="choose-a-memory-analysis-tool-in-visual-studio-c-visual-basic-c-f"></a>使用 C#、Visual Studio (、Visual Basic、C++、F#) 

可以使用多种工具查找内存泄漏和低效内存使用情况，例如集成了调试程序的“内存使用情况”诊断工具，或性能探查器中的工具（如 .NET 对象分配工具和事后分析“内存使用情况”工具）。

通过内存使用率工具可以拍摄托管和本机内存堆的一个或多个快照  。 可收集 .NET、ASP.NET、C++ 或混合模式（.NET 和本机）应用的快照。 “内存使用情况”工具可以在打开的 Visual Studio 项目和已安装的 Microsoft Store 应用上运行，也可以附加到正在运行的应用或进程。 无论是否进行调试，都可以运行“内存使用情况”工具。 有关详细信息，请参阅[运行带或不带调试器的分析工具](../profiling/running-profiling-tools-with-or-without-the-debugger.md)。 在调试程序中，你可以打开和关闭内存分析，并查看按每个对象细分的内存使用情况。 可以在暂停执行时（例如在断点处）查看内存使用情况结果。

.NET 开发人员可以在 .NET 对象分配工具或[内存使用](../profiling/memory-usage.md)工具之间进行选择。

- [.NET 对象分配工具](../profiling/dotnet-alloc-tool.md)有助于识别 .NET 代码中的分配模式和异常，并有助于识别垃圾回收的常见问题。 此工具仅作为事后分析工具运行。 可以在本地或远程计算机上运行此工具。
- [内存使用工具](../profiling/memory-usage-without-debugging2.md)有助于识别 .NET 应用中并不常见的内存泄漏。 如果需要在检查内存时使用调试器功能，如单步执行代码，则建议使用[集成了调试器的内存使用](../profiling/memory-usage.md)工具。

C++ 开发人员可以使用集成了调试器的或非调试器的内存使用工具。

- [使用调试器分析内存使用情况](../profiling/memory-usage.md)
- [分析不调试的内存使用情况](../profiling/memory-usage-without-debugging2.md)

可 Windows 7 及更高版本中使用不带调试器的分析工具。 要运行带调试器的分析工具（“诊断工具”窗口），需具备 Windows 8 及更高版本。

## <a name="blogs-and-videos"></a>博客和视频

[调试时分析 CPU 和内存](https://devblogs.microsoft.com/visualstudio/analyze-cpu-memory-while-debugging/)

[Visual C++ 博客：Visual C++ 2015 中的内存分析](https://devblogs.microsoft.com/cppblog/memory-profiling-in-visual-c-2015/)

## <a name="see-also"></a>请参阅

- [使用 Visual Studio 分析](../profiling/index.yml)
- [首先了解分析工具](../profiling/profiling-feature-tour.md)
