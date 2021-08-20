---
title: 了解资源争用数据值 | Microsoft Docs
description: 了解资源争用分析如何收集当应用程序中的争用线程访问共享资源时被强制等待的详细信息。
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 80e525b078fb5743d9181361d26230faf740c01a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122140788"
---
# <a name="understand-resource-contention-data-values"></a>了解资源争用数据值

资源争用分析将收集每次应用程序中的争用线程访问共享资源时被强制等待的详细调用堆栈信息。

资源争用报告显示争用的总数，以及对于在其中发生等待的模块、函数、源代码行和指令，等待资源所用的总时间。

- 非独占值显示资源争用迫使函数等待的争用总数以及函数等待的总时间。  非独占值包括函数调用的子函数导致的争用。

- 独占值只显示迫使函数等待并且由函数体中的代码导致的争用数。 不包括子函数导致的争用。 函数的独占时间也只包括函数体中的语句导致的等待时间。

资源争用报告视图还包括显示一段时间内各个争用事件的时间线关系图，并显示创建特定事件的调用堆栈。 有关更多信息，请参见下列主题之一：

- [线程详细信息视图](../profiling/thread-details-view-contention-data.md)

- [资源详细信息视图](../profiling/resource-details-view-contention-data.md)

有关并发分析的第二个模式的详细信息，请参阅[并发可视化工具](../profiling/concurrency-visualizer.md)。
