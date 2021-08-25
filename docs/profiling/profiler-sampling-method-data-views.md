---
title: 探查器采样方法数据视图 | Microsoft Docs
description: 了解使用采样方法生成的探查器数据文件的视图和报表的参考信息。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools,sampling data views
- sampling data views
ms.assetid: 798de693-e43a-4056-aff5-48310c2172c5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 4ae6d510c68a1e3ea8e9f2c0f66b9b5bac3071c2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122131217"
---
# <a name="profiler-sampling-method-data-views"></a>探查器采样方法数据视图
本节包含有关使用采样方法生成的探查器数据文件的视图和报告的参考信息。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

## <a name="in-this-section"></a>本节内容
- [“摘要”视图](../profiling/summary-view-sampling-data.md)

 列出收集样本时执行频率最高的函数，以及执行单个工作最多的函数。

- [“调用树”视图](../profiling/call-tree-view-sampling-data.md)

 显示层次结构树中各个函数的执行路径。

- [“模块”视图](../profiling/modules-view-sampling-data.md)

 按模块组织分析数据，并列出函数、源代码行和收集样本时执行的说明。

- [“调用方/被调用方”视图 - 采样数据](../profiling/caller-callee-view-sampling-data.md)

 显示所选函数和调用所选函数及被所选函数调用的函数之间的分析数据。

- [“函数”视图](../profiling/functions-view-sampling-data.md)

 按函数组织分析数据，并列出收集样本时执行的函数。

- [“行”视图](../profiling/lines-view-sampling-data.md)

 列出收集样本时执行的源代码行。

- [“指令指针”(IP) 视图](../profiling/instruction-pointers-ips-view-sampling-data.md)

 列出收集样本时执行的源代码行。

## <a name="reference"></a>参考
- [“进程”视图](../profiling/process-view.md)

 列出进程和线程的开始和结束时间。

- [“标记”视图](../profiling/marks-view.md)

 列出插入到分析数据文件的 ETW 和采样事件。

- [“函数详细信息”视图](../profiling/function-details-view.md)

 显示所选函数和调用所选函数及被所选函数调用的函数之间的关系图形图表。

## <a name="related-sections"></a>相关章节
- [检测方法数据视图](../profiling/instrumentation-method-data-views.md)

 关于使用检测方法生成的探查器数据文件的视图和报表的参考信息。

- [.NET 内存数据视图](../profiling/dotnet-memory-data-views.md)

 有关包含 .NET 内存数据的探查器数据文件的视图和报告的参考信息。

## <a name="see-also"></a>另请参阅
- [了解采样数据值](../profiling/understanding-sampling-data-values.md)
