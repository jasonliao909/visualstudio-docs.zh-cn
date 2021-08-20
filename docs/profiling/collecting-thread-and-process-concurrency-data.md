---
title: 收集线程和进程并发数据
description: 使用分析工具并发分析方法收集导致函数等待访问资源的每个同步事件的相关数据。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- concurrency profiling method
- Profiling Tools, concurrency method
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: cdcefa6559aea6ed59bb2097e2a2285eabc4b07a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122142320"
---
# <a name="collect-thread-and-process-concurrency-data"></a>收集线程和进程并发数据

通过 Visual Studio 分析工具并发分析方法，可以收集资源争用数据，其中包括有关导致所分析应用程序中的函数等待访问资源的每个同步事件的信息。

可以使用以下步骤之一来指定并行分析方法：

- 在“分析向导”的第一页上，单击“并发” 
- 在性能会话的属性对话框的“常规”  页上，选择“并发”  。
- 在“性能资源管理器”  工具栏上的“方法”  列表中，单击“并发”  。

## <a name="common-tasks"></a>常见任务

可以指定 _性能会话_  对话框中的附加选项。 若要打开此对话框：

- 在“性能资源管理器”  中，右键单击性能会话名称，然后单击“属性”  。

下表中的任务描述了在使用并发方法进行分析时，可以在性能会话的“属性页”对话框中指定的选项。

|任务|相关内容|
|----------|---------------------|
|在“常规”  页上，为生成的分析数据 (.vsp) 文件指定命名详细信息。|- [如何：设置性能数据文件名选项](../profiling/how-to-set-performance-data-file-name-options.md)|
|如果代码解决方案中具有多个 .exe 项目，请在“启动”  页上指定要启动的应用程序。|- [如何：指定要启动的二进制文件](../profiling/how-to-specify-the-binary-to-start.md)|
|在“层交互”  页上，将 ADO.NET 调用数据添加到分析运行中。|- [收集层交互数据](../profiling/collecting-tier-interaction-data.md)|
|在“Windows 计数器”  页上，指定要作为标记添加到分析数据的一个或多个操作系统性能计数器。|- [如何：收集 Windows 计数器数据](../profiling/how-to-collect-windows-counter-data.md)|
|如果应用程序模块使用多个版本，请在“高级”  页上指定要分析的 .NET Framework 运行时的版本。 默认情况下会分析加载的第一个版本。|- [如何：指定 .NET Framework 运行时](../profiling/how-to-specify-the-dotnet-framework-runtime.md)|
