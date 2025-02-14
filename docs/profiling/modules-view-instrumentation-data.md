---
title: “模块”视图 - 检测数据 | Microsoft Docs
description: 了解“模块”视图如何显示按分析数据中的模块分组的性能数据。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Modules view
ms.assetid: 895b9589-1987-4160-916f-53b898a69cf0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 9b2139b9483253507f926d9ac0ef37bba155f666
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736288"
---
# <a name="modules-view---instrumentation-data"></a>“模块”视图 - 检测数据
“模块”视图显示按分析数据中的模块分组的性能数据。 模块的各函数在模块节点下列出。

## <a name="general"></a>常规
 常规列标识视图行中的函数。

|列|说明|
|------------|-----------------|
|**名称**|函数或模块的名称。|
|**函数行号**|此函数在源文件中的起始行号。|
|**调用数**|对此函数或模块进行的调用总数。|
|**源文件**|此函数的定义所在的源文件。|
|**模块名**|函数所在模块的名称。|
|**模块路径**|函数所在模块的路径。|
|**进程 ID**|分析运行的进程 ID (PID)。|
|**进程名**|在其中执行模块或函数的进程的名称。|
|**时间独占探测开销**|此函数或模块由检测导致的时间开销。|
|**时间非独占探测开销**|此函数或模块及其子函数由检测导致的时间开销。|

## <a name="elapsed-inclusive-values"></a>已用非独占值
 已用非独占值表示函数位于调用堆栈上的时间。 此时间包括子函数中和对操作系统的调用中所用的时间，如上下文切换和输入/输出操作。

|列|描述|
|------------|-----------------|
|**已用非独占时间**|-   对于函数，是此函数中所用的时间。 这包括子函数中和对操作系统的调用中所用的时间，如上下文切换和输入/输出操作。<br />-   对于模块，是模块中的至少一个函数处于调用堆栈中的时间。|
|**已用非独占时间百分比**|此模块或函数的总已用非独占时间占分析运行期间所用的总已用非独占时间的百分比。|
|**平均已用非独占时间**|-   对于函数，是对此函数的调用的平均已用非独占时间。<br />-   对于模块，是对此模块中函数的所有调用的平均已用非独占时间。|
|**最长已用非独占时间**|-   对于函数，是对此函数的调用的最长已用非独占时间。<br />-   对于模块，是对此模块中函数的所有调用的最长已用非独占时间。|
|**最短已用非独占时间**|-   对于函数，是对此模块或函数的调用的最短已用非独占时间。<br />-   对于模块，是对此模块中函数的所有调用的最短已用非独占时间。|

## <a name="elapsed-exclusive-values"></a>已用独占值
 已用独占值表示函数在调用堆栈顶部直接执行的时间。 此时间包括对操作系统的调用所用的时间，如上下文切换和输入/输出操作，但不包括子函数所用的时间。

|列|描述|
|------------|-----------------|
|**已用独占时间**|-   对于函数，是此模块或函数中所用的时间。 这包括对操作系统的调用，如上下文切换和输入/输出操作，但不包括子函数中所用的时间。<br />-   对于模块，是此模块中函数的已用独占时间之和。|
|**已用独占时间百分比**|此模块或函数的总已用独占时间占分析运行期间所用的总已用独占时间的百分比。|
|**平均已用独占时间**|-   对于函数，是对此函数的调用的平均已用独占时间。<br />-   对于模块，是对此模块中函数的所有调用的平均已用独占时间。|
|**最长已用独占时间**|-   对于函数，是对此函数的调用的最长已用独占时间。<br />-   对于模块，是对此模块中函数的所有调用的最长已用独占时间。|
|**最短已用独占时间**|-   对于函数，是对此模块或函数的调用的最短已用独占时间。<br />-   对于模块，是对此模块中函数的所有调用的最短已用独占时间。|

## <a name="application-inclusive-values"></a>应用程序非独占值
 应用程序非独占值表示函数位于调用堆栈上的时间。 此时间不包括对操作系统的调用中所用的时间，如上下文切换和输入/输出操作。但是，此时间包括子函数中所用的时间。

|列|描述|
|------------|-----------------|
|**应用程序非独占时间**|-   对于函数，是对此函数的调用中所用的时间。 这包括子函数中所用的时间，但不包括对操作系统的调用，如上下文切换和输入/输出操作。<br />-   对于模块，是模块中的至少一个函数处于调用堆栈中的时间。 这不包括对操作系统的调用中所用的时间。|
|**应用程序非独占时间百分比**|此模块或函数的应用程序非独占时间占分析运行期间所用的总已用非独占时间的百分比。|
|**平均应用程序非独占时间**|-   对于函数，是对此函数的调用的平均应用程序非独占时间。<br />-   对于模块，是对此模块中函数的所有调用的平均应用程序非独占时间。|
|**最长应用程序非独占时间**|-   对于函数，是对此函数的调用的最长应用程序非独占时间。<br />-   对于模块，是对此模块中函数的所有调用的最长应用程序非独占时间。|
|**最短应用程序非独占时间**|-   对于函数，是对此模块或函数的调用的最短应用程序非独占时间。<br />-   对于模块，是对此模块中函数的所有调用的最短应用程序非独占时间。|

## <a name="application-exclusive-values"></a>应用程序独占值
 应用程序独占值表示此模块或函数中所用的时间。 此值不包括子函数中所用的时间，也不包括对操作系统的调用，如上下文切换和输入/输出操作。

|列|描述|
|------------|-----------------|
|**应用程序独占时间**|对此模块或函数的所有调用的总应用程序独占时间。|
|**应用程序独占时间百分比**|此模块或函数的应用程序独占时间占分析运行期间所用的总已用独占时间的百分比。|
|**平均应用程序独占时间**|-   对于函数，是对此函数的调用的平均应用程序独占时间。<br />-   对于模块，是对此模块中函数的所有调用的平均应用程序独占时间。|
|**最长应用程序独占时间**|-   对于函数，是对此函数的调用的最长应用程序独占时间。<br />-   对于模块，是对此模块中函数的所有调用的最长应用程序独占时间。|
|**最短应用程序独占时间**|-   对于函数，是对此模块或函数的调用的最短应用程序独占时间。<br />-   对于模块，是对此模块中函数的所有调用的最短应用程序独占时间。|

## <a name="see-also"></a>另请参阅
- [“模块”视图](../profiling/modules-view-sampling-data.md)
- [“模块”视图 - 检测](../profiling/modules-view-dotnet-memory-instrumentation-data.md)
- [“模块”视图 - 采样](../profiling/modules-view-dotnet-memory-sampling-data.md)
