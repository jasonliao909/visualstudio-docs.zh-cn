---
title: “调用方 - 被调用方”视图 - .NET 内存检测数据 | Microsoft Docs
description: 查看 .NET 内存分析数据的“调用方/被调用方”视图，该视图显示所选函数及其父函数和子函数的分配和计时数据。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Caller/Callee view
ms.assetid: da624c06-8741-4afb-aad1-f8c0002f3de2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: f3558ef81017fe382c5729003be8f1dd80978135
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736658"
---
# <a name="callercallee-view---net-memory-instrumentation-data"></a>“调用方/被调用方”视图 - .NET 内存检测数据
通过使用检测方法收集 .NET 内存分析数据的“调用方/被调用方”视图，此视图显示所选函数的分配和计时数据及该所选函数的父函数和子函数。 “调用方/被调用方”视图包含三个网格。

 **当前函数** 在中间网格中显示，并且显示所选函数的内存分析信息。 这些值包括对函数的所有采样调用。

 **调用当前函数的函数** 在顶部网格中显示，并且显示由调用方（父）函数的调用生成的所选（当前）函数的值的量。

 **由当前函数调用的函数** 在底部网格中显示，并且在当前函数调用子函数时，它显示所选函数的被调用方（子）函数的内存分析数据。

 双击调用方或被调用方函数行，以使该行成为当前函数。

## <a name="general"></a>常规

|列|描述|
|------------|-----------------|
|**函数名**|函数名。|
|**函数地址**|函数的地址。|
|**函数行号**|此函数在源文件中的起始行号。|
|**调用数**|对此函数进行的调用总数。|
|**源文件**|此函数的定义所在的源文件。|
|**模块名**|函数所在模块的名称。|
|**模块路径**|函数所在模块的路径。|
|**进程 ID**|分析运行的进程 ID。|
|**进程名**|分配给进程的名称。|
|**时间独占探测开销**|此函数由检测导致的时间开销。 已从所有独占时间中减去探测开销。|
|**时间非独占探测开销**|此函数及其子函数由检测导致的时间开销。 已从所有非独占时间中减去探测开销。|
|**Type**|函数的上下文：<br /><br /> **0** - 当前函数<br /><br /> **1** - 调用当前函数的函数<br /><br /> **2** - 当前函数调用的函数<br /><br /> 仅在 [VSPerfReport](../profiling/vsperfreport.md) 命令行报表中。|
|**根函数名**|当前函数的名称。 仅在 [VSPerfReport](../profiling/vsperfreport.md) 命令行报表中。|

## <a name="net-memory-allocation-values"></a>.NET 内存分配值

|列|描述|
|------------|-----------------|
|**独占分配数**|-   对于当前函数，是函数在函数体中执行代码时（即函数位于调用堆栈顶部时）创建的对象数。 此数值不包括此函数调用的函数中创建的对象数。<br />-   对于调用方函数，是此调用方函数的调用生成的当前函数的独占分配数。<br />-   对于被调用方函数，是由当前函数调用的此函数的实例所创建的对象数。 此数值不包括被调用方函数调用的函数所创建的对象数。|
|**独占分配数百分比**|分析运行期间创建的属于此函数的独占分配的所有对象数的百分比。|
|**非独占分配数**|-   对于当前函数，是分析运行期间函数分配的对象数。 此数值包括由函数调用的被调用方函数中创建的对象数。<br />-   对于调用方函数，是此调用方函数的调用生成的当前函数的非独占分配数。<br />-   对于被调用方函数，是当前函数的调用生成的此函数的实例所分配的对象数。 此数值包括此被调用方函数调用的函数所进行的分配。|
|**非独占分配数百分比**|分析运行期间创建的属于此函数的非独占分配的所有对象数的百分比。|
|**独占字节数**|-   对于当前函数，是分析运行期间函数分配的内存字节数。 此数值不包括函数调用的被调用方函数中分配的内存。<br />-   对于调用方函数，是此调用方函数的调用生成的当前函数的独占字节数。<br />-   对于被调用方函数，是由当前函数的调用生成的此函数的实例所分配的字节数。 此数值不包括被调用方函数调用的函数所分配的字节数。|
|**独占字节数百分比**|分析运行期间分配的属于此函数的独占分配的所有内存字节数的百分比。|
|**非独占字节数**|-   对于当前函数，是分析运行期间函数分配的内存字节数。 此数值包括函数调用的被调用方函数中所分配的内存。<br />-   对于调用方函数，是此调用方函数的调用生成的当前函数的实例的非独占字节数。<br />-   对于被调用方函数，是由当前函数的调用生成的此函数的实例所分配的字节数。 此数值包括此被调用方函数调用的函数所分配的字节数。|
|**非独占字节数百分比**|分析运行期间分配的属于此函数的非独占分配的所有内存字节数的百分比。|

## <a name="elapsed-inclusive-values"></a>已用非独占值
 已用非独占值表示函数位于调用堆栈上的时间。 此时间包括子函数中和对操作系统的调用中所用的时间，如上下文切换和输入/输出操作。

|列|描述|
|------------|-----------------|
|**已用非独占时间**|-   对于当前函数，是函数中所用的时间。 此值包括子函数中和调用操作系统所用的时间，如上下文切换和输入/输出操作。<br />-   对于调用方函数，是此调用方函数的调用生成的当前函数的已用非独占时间量。<br />-   对于被调用方函数，是当前函数的调用生成的此函数所用的时间。 此值包括子函数中和调用操作系统所用的时间，如上下文切换和输入/输出操作。|
|**已用非独占时间百分比**|本上下文中此函数的已用非独占时间占分析运行期间所用的总已用非独占时间的百分比。|
|**平均已用非独占时间**|本上下文中对此函数的调用的平均已用非独占时间。|
|**最长已用非独占时间**|本上下文中对此函数的调用的最长已用非独占时间。|
|**最短已用非独占时间**|本上下文中对此函数的调用的最短已用非独占时间。|

## <a name="elapsed-exclusive-values"></a>已用独占值
 已用独占值表示函数在调用堆栈顶部直接执行的时间。 此时间包括对操作系统的调用所用的时间，如上下文切换和输入/输出操作，但不包括子函数所用的时间。

|列|描述|
|------------|-----------------|
|**已用独占时间**|-   对于当前函数，是执行函数体所用的时间。 此值不包括子函数中所用的时间，但包括对操作系统的调用所用的时间，如上下文切换和输入/输出操作。<br />-   对于调用方函数，是此调用方函数的调用生成的当前函数的已用独占时间量。<br />-   对于被调用方函数，是当前函数的调用生成的此函数所用的时间。 此值不包括被调用方函数的子函数中所用的时间，但包括对操作系统的调用所用的时间，如上下文切换和输入/输出操作。|
|**已用独占时间百分比**|本上下文中此函数的总已用独占时间占分析运行期间所用的总已用独占时间的百分比。|
|**平均已用独占时间**|本上下文中对此函数的调用的平均已用独占时间。|
|**最长已用独占时间**|本上下文中对此函数的调用的最长已用独占时间。|
|**最短已用独占时间**|本上下文中对此函数的调用的最短已用独占时间。|

## <a name="application-inclusive-values"></a>应用程序非独占值
 应用程序非独占值表示函数位于调用堆栈上的时间。 此时间不包括对操作系统的调用中所用的时间，如上下文切换和输入/输出操作，但包括子函数中所用的时间。

|列|描述|
|------------|-----------------|
|**应用程序非独占时间**|-   对于当前函数，是函数及其子函数所用的时间。 此值不包括调用操作系统所用的时间，如上下文切换和输入/输出操作。<br />-   对于调用方函数，是此调用方函数的调用生成的当前函数的应用程序非独占时间量。<br />-   对于被调用方函数，是当前函数的调用生成的此函数及其子函数所用的时间。 此值不包括对操作系统的调用所用的时间，如上下文切换和输入/输出操作。|
|**应用程序非独占时间百分比**|本上下文中此函数的总应用程序非独占时间占分析运行期间所用的总已用非独占时间的百分比。|
|**平均应用程序非独占时间**|本上下文中对此函数的调用的平均应用程序非独占时间。|
|**最长应用程序非独占时间**|本上下文中对此函数的调用的最长应用程序非独占时间。|
|**最短应用程序非独占时间**|本上下文中对此函数的调用的最短应用程序非独占时间。|

## <a name="application-exclusive-values"></a>应用程序独占值
 应用程序独占值表示函数中所用的时间，不包括子函数中所用的时间。 此表示值也不包括对操作系统的调用所用的时间，如上下文切换和输入/输出操作。

|列|描述|
|------------|-----------------|
|**应用程序独占时间**|-   对于当前函数，是执行函数体所用的时间。 此值不包括子函数中所用的时间，也不包括对操作系统的调用所用的时间，如上下文切换和输入/输出操作。<br />-   对于调用方函数，是此调用方函数的调用生成的当前函数的应用程序独占时间量。<br />-   对于被调用方函数，是当前函数的调用生成的此函数所用的时间。 此值不包括被调用方函数的子函数中所用的时间，也不包括对操作系统的调用所用的时间，如上下文切换和输入/输出操作。|
|**应用程序独占时间百分比**|本上下文中此函数的总应用程序独占时间占分析运行期间所用的总已用独占时间的百分比。|
|**平均应用程序独占时间**|本上下文中对此函数的调用的平均应用程序独占时间。|
|**最长应用程序独占时间**|本上下文中对此函数的调用的最长应用程序独占时间。|
|**最短应用程序独占时间**|本上下文中对此函数的调用的最短应用程序独占时间。|

## <a name="see-also"></a>请参阅
- [如何：自定义报表视图列](../profiling/how-to-customize-report-view-columns.md)
- [“调用方/被调用方”视图 - .NET 内存采样数据](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)
- [“调用方/被调用方”视图 - 检测数据](../profiling/caller-callee-view-instrumentation-data.md)
- [“调用方/被调用方”视图 - 采样数据](../profiling/caller-callee-view-sampling-data.md)
