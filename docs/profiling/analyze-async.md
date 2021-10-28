---
title: 分析 .NET 异步代码的性能 | Microsoft Docs
description: 使用 .NET 异步工具来分析异步代码中的性能。 列出的每项任务都有计时。 要查看代码，请使用“转到源文件”。
ms.custom: SEO-VS-2020
ms.date: 5/5/2020
ms.topic: conceptual
helpviewer_keywords:
- asynchronous, async, profiling
author: esteban-herrera
ms.author: esherrer
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 86575cd71c41ac8ac874e9b62f8273ee46e02c57
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126642431"
---
# <a name="analyze-performance-of-net-asynchronous-code"></a>分析 .NET 异步代码的性能

使用 .NET Async 工具来分析应用中异步代码的性能。

> [!NOTE]
> .NET Async 工具需要 Visual Studio 2019 版本 16.7 或更高版本，以及使用 async 和 await 的 .NET 项目。

## <a name="setup"></a>安装

1. 在 Visual Studio 中，按 Alt+F2 打开性能探查器。

1. 选中“.NET Async”复选框。

   ![已选中“.NET Async”工具](../profiling/media/async-tool-selected.png "已选中“.NET Async”工具")

1. 单击“启动”按钮，运行该工具。

1. 在此工具开始运行后，在应用中完成要探查的方案。 然后，选择“停止收集”或关闭应用，以查看数据。

1. 在收集停止后，就会看到一个表，其中包含在分析会话期间发生的活动。

   ![.NET Async 工具已停止](../profiling/media/async-tool-opened.png ".NET Async 工具已停止")

异步事件整理为按时间顺序划分的活动。 每个活动都显示它的开始时间、结束时间和持续时间。

与[任务](/dotnet/api/system.threading.tasks)对应的每一行都在“名称”列中有“任务”标签。 对于无法解析的任何任务名称，显示的是“任务属于”标签。 后跟任务所在方法的名称。 如果异步活动在收集会话期间没有完成，则“结束时间”列中显示“未完成”标签。

若要进一步调查特定的任务或活动，请右键单击相应行。 然后，选择“转到源文件”，以查看活动在代码中的何处发生。

![.NET Async 工具（选择了“转到源文件”）](../profiling/media/async-tool-gotosource.png ".NET Async 工具（选择了“转到源文件”）")

## <a name="see-also"></a>请参阅

- [优化探查器设置](../profiling/optimize-profiler-settings.md)