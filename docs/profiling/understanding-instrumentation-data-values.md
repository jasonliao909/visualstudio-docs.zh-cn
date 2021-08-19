---
title: 了解检测数据值 | Microsoft Docs
description: 了解检测分析方法如何记录所分析应用程序中函数调用、行和指令的详细计时信息。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools,instrumentation
- instrumentation profiling method
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 751d990a7b7e3623311fd7487e0303100ec7300a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122140812"
---
# <a name="understand-instrumentation-data-values"></a>了解检测数据值

Visual Studio 的检测分析方法会记录所分析应用程序中函数调用、行和指令的详细计时信息

检测方法会在所分析二进制文件中的目标函数开头和末尾注入代码，并且是在这些函数每次调用到其他函数之前和之后注入。 注入的代码会记录以下信息：

- 此收集事件和前一个事件之间的间隔。

- 操作系统是否在此间隔中执行了操作。 例如，操作系统可能会对磁盘进行读取或写入，或是在目标线程与其他进程中的其他线程之间切换。

对于每个间隔，探查器分析会在间隔结束时重新构造已存在的调用堆栈。 调用堆栈是某个时间点在处理器中处于活动状态的函数的列表。 只有一个函数（当前函数）在执行代码；其他函数是在调用当前函数时产生的函数调用链（调用堆栈）。

对于记录间隔时调用堆栈中的每个函数，探查器分析会将间隔添加到函数的四个数据值中的一个或多个。 分析基于两个条件将间隔添加到函数的数据值：

- 间隔是在函数的代码中还是在子函数（函数调用的函数）中出现。

- 在间隔中是否发生了操作系统事件。

函数或数据范围的间隔的数据值称为已用非独占、已用独占、应用程序非独占和应用程序独占：

- 函数的所有间隔都会添加到已用非独占数据值。

- 如果间隔在函数的代码中，而不在子函数中出现，则间隔会添加到函数的已用独占数据值。

- 如果在间隔中未发生操作系统事件，则间隔会添加到应用程序非独占数据值。

- 如果在间隔中未发生操作系统事件，并且此间隔出现在函数代码的直接执行中（即，未出现在子函数中），则间隔会添加到应用程序独占数据值。

分析工具报告会汇总分析会话本身中的函数以及会话的进程、线程和二进制文件的总计值。

## <a name="elapsed-inclusive-values"></a>已用非独占值

执行某个函数及其子函数所用的总时间。

已用非独占值包括直接执行函数代码所用的间隔以及执行目标函数的子函数所用的间隔。 已用非独占值还包括该函数或其子函数的包含等待操作系统的间隔。

## <a name="elapsed-exclusive-values"></a>已用独占值

执行某个函数所用的时间，不包括在子函数中所用的时间。

已用独占值包括直接执行函数代码所用的间隔，而不考虑是否在间隔中发生了操作系统事件。 已用独占值不包括在目标函数调用的子函数中所用的所有间隔。

## <a name="application-inclusive-values"></a>应用程序非独占值

执行某个函数及其子函数所用的时间，不包括在操作系统事件中所用的时间。

应用程序非独占值不包括包含操作系统事件的间隔。 应用程序非独占值包括执行函数所用的所有其他间隔，而不考虑间隔是用于直接执行函数代码还是用于目标函数的子函数。

## <a name="application-exclusive-values"></a>应用程序独占值

执行某个函数所用的时间，不包括在子函数中所用的时间以及在操作系统事件中所用的时间。

应用程序独占值不包括包含操作系统事件的间隔或执行该函数调用的函数所用的间隔。 应用程序独占值仅包括直接执行函数代码所用的并且不包含操作系统事件的间隔。

## <a name="elapsed-inclusive-percent"></a>已用非独占百分比

函数、模块、线程或进程的已用非独占值占分析会话的总已用非独占值的百分比。

100 * 函数已用非独占值/会话已用非独占值

## <a name="elapsed-exclusive-percent"></a>已用独占百分比

函数、模块、线程或进程的已用独占值占分析会话的总已用非独占值的百分比。

100 * 函数已用独占值/会话已用非独占值

## <a name="application-inclusive-percent"></a>应用程序非独占百分比

函数、模块、线程或进程的应用程序非独占值占分析会话的总应用程序非独占值的百分比。

100 * 函数应用程序非独占值/会话应用程序非独占值

## <a name="application-exclusive-percent"></a>应用程序独占百分比

函数、模块、线程或进程的应用程序独占间隔占分析会话的总应用程序非独占值的百分比。

100 * 函数应用程序独占值/会话应用程序非独占值

## <a name="see-also"></a>另请参阅

[分析性能工具数据](../profiling/analyzing-performance-tools-data.md)
[如何：选择收集方法](../profiling/how-to-choose-collection-methods.md)
