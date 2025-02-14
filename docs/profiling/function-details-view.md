---
title: 函数详细信息视图 | Microsoft Docs
description: 在性能资源管理器中，了解“函数详细信息视图”窗口、开销分布条形图、“函数性能详细信息”表和“函数代码视图”窗口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.functiondetails
helpviewer_keywords:
- Function Details view
- Profiling Tools, Function Details view
ms.assetid: 8806954f-cf28-48d5-81b2-d722ceaf7d27
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 98771014f903b88ad57ec8713fd2867094c483b2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736187"
---
# <a name="function-details-view"></a>函数详细信息视图
“函数详细信息视图”窗口显示以下信息：

- “开销分布”条形图表示所选函数与执行所选函数的调用函数之间的关系，以及所选函数与其调用的其他函数之间的关系。

- “函数性能详细信息”表，该表显示所指定函数的摘要分析数据。

- “函数代码视图”窗口，该窗口在代码可用时显示函数代码。

  “函数代码视图”窗口是一个独立的窗格。 默认情况下，这两个窗格沿水平方向拆分，而“函数代码视图”窗口位于框架的底部。

- 若要沿垂直方向拆分两个窗格，请单击工具栏上的“垂直拆分屏幕”。

- 若要更改窗格的相对大小，请单击框架之间的阴影边框，并将该边框拖至其他位置。

## <a name="cost-distribution-bar-chart"></a>开销分布条形图

### <a name="performance-metrics"></a>性能指标
 在“性能指标”下拉列表中，可指定视图中显示哪些值。 可用的值取决于在分析数据文件中使用的分析方法。 括号中的名称是“函数性能详细信息”表中各行的名称。

### <a name="bar-chart"></a>条形图
 **调用函数**

 “调用函数”条显示调用所选函数的函数。 调用函数所在块的大小与该调用函数在所选函数的性能总度量值中所占的份额成比例。

 可单击调用函数的名称，使其成为视图中的所选函数。

- 如果要列出的调用函数过多，则在“其他”块中收集所占份额最少的函数。 单击“其他”可在“调用方/被调用方视图”窗口中显示所选函数的所有调用和被调用函数。 有关详细信息，请参阅[“调用方/被调用方”视图](../profiling/caller-callee-view.md)。

- 如果没有任何调用函数，或该函数是线程或进程的入口函数，则会显示“堆栈顶部”块。

  **所选函数**

  所选函数栏显示被调用函数及所选函数中代码在所选函数的性能总度量值中所占的份额。 被调用函数所在块或函数体的大小与其在所选函数的性能总度量值中所占的份额成比例。

  可单击被调用函数的名称，使其成为视图中的所选函数。

- “总计”值是所选函数的性能指标。

- “函数体”块表示直接执行函数体内代码时产生的性能总度量值的量。

- 块中列出了由所选函数调用的函数。 所选函数块的大小表示所选函数在被调用函数中产生的性能总度量值的量。

- 如果要列出的调用函数过多，则在“其他”块中收集所占份额最少的函数。 单击“其他”可在“调用方/被调用方视图”窗口中显示所选函数的所有调用和被调用函数。 有关详细信息，请参阅[“调用方/被调用方”视图](../profiling/caller-callee-view.md)。

- 如果没有任何被调用函数，则显示“堆栈底部”块。

## <a name="function-performance-details"></a>函数性能详细信息
 “函数性能详细信息”表提供所选函数的性能指标的摘要数据。 同时显示值和百分比。 在“性能指标”列表中指定图表和详细信息表中显示的分析数据。

|列|描述|
|------------|-----------------|
|**独占**|- 执行函数体时产生的性能指标的量。|
|**在调用中**|- 所选函数所调用的函数中产生的性能指标的量。|
|**非独占总数**|-“独占”和“在调用中”值的总和。|

## <a name="function-code-view"></a>函数代码视图
 “函数代码视图”窗口显示源代码的列表（列表可用时）。 调用其他函数的源代码行旁边是一个有阴影的列，该列包含被调用函数的性能指标值。 若要编辑源代码，请单击源代码文件的链接。

## <a name="cost-distribution-bar-chart-values"></a>开销分布条形图值

### <a name="sampling"></a>采样
 下表介绍了“性能指标”列表中使用采样方法收集的分析数据的值。

|“值”|描述|
|-|-|
|**非独占样本数（收集的样本）**|- 对于调用函数，为此调用函数调用所选函数时收集的样本的数量。<br />- 对于函数体，为所选函数在执行其自身代码时收集的样本数。<br />- 对于被调用函数，为因所选函数发生调用而执行被调用函数时收集的样本数。|

### <a name="instrumentation"></a>检测
 下表介绍了“性能指标”列表中使用检测方法收集的分析数据的值。

|“值”|描述|
|-|-|
|**已用非独占时间（已用时间）**|已用时间包括调用操作系统所用的时间，如上下文切换和输入/输出操作。<br /><br /> - 对于 **调用函数**，为执行此函数调用的所选函数实例所用的已用时间量。 包括由所选函数调用的函数所用的时间。<br />- 对于 **函数体**，为执行所选函数的代码所用的已用时间总量。 不包括被调用函数所用的时间。<br />- 对于被调用函数，为执行所选函数调用的函数实例所用的时间量。 总时间包括该函数调用的函数所用的时间。 包括由所选函数调用的函数所用的时间。|
|**应用程序非独占时间（应用程序时间）**|应用程序时间不包括调用操作系统所用的时间，如上下文切换和输入/输出操作。<br /><br /> - 对于 **调用函数**，为执行此函数调用的所选函数实例所用的应用程序时间量。 包括由所选函数调用的函数所用的时间。<br />- 对于 **函数体**，为执行所选函数的代码所用的应用程序时间总量。 不包括被调用函数所用的时间。<br />- 对于被调用函数，为执行所选函数调用的函数实例所用的应用程序时间量。 总时间包括该函数调用的函数所用的时间。|

### <a name="net-memory"></a>.NET 内存
 下表介绍了“性能指标”列表中使用 .NET 内存分析方法收集的分析数据的值。

|“值”|描述|
|-|-|
|**非独占分配数（分配数）**|- 对于 **调用函数**，为由该函数调用的所选函数实例分配的对象数量。 此数量包括由所选函数调用的函数分配的对象。<br />- 对于 **函数体**，为所选函数在执行其自身代码时分配的对象数量。 不包括由所选函数调用的函数中分配的对象。<br />- 对于被调用的函数，为由所选函数调用的函数实例所分配的对象数。 此数量包括由该函数调用的函数分配的对象。|
|**非独占字节数（字节数）**|- 对于 **调用函数**，为由该函数调用的所选函数实例分配的字节数量。 此数量包括由所选函数调用的函数分配的字节。<br />- 对于 **函数体**，为所选函数在执行其自身代码时分配的总字节数量。 不包括由所选函数调用的函数中分配的字节。<br />- 对于被调用的函数，为由所选函数调用的函数实例所分配的字节数。 此数量包括由该函数调用的函数分配的字节。|

### <a name="concurrency"></a>并发
 下表介绍了“性能指标”列表中使用并发方法收集的分析数据的值。

|“值”|描述|
|-|-|
|**非独占争用数（争用数）**|- 对于 **调用函数**，为由该函数调用的所选函数实例中发生的资源争用事件数。 此数量包括由所选函数调用的函数中的争用事件。<br />- 对于 **函数体**，为该函数执行自身代码时发生的争用事件总数。 不包括由所选函数调用的函数中发生的争用。<br />- 对于被调用函数，为所选函数调用的函数实例中发生的争用事件数。 此数量包括该函数调用的函数中发生的争用事件。|
|**非独占阻塞的时间（阻塞时间）**|- 对于调用函数，为该函数调用的所选函数实例的资源争用事件所用的时间。 此时间包括所选函数调用的函数中的阻塞时间。<br />- 对于 **函数体**，为该函数执行自身代码时发生的争用事件中所用的总时间。 不包括所选函数调用的函数中发生的争用。<br />- 对于被调用函数，为所选函数调用的函数实例的资源争用事件中所用的时间。 此时间包括该函数调用的函数中发生的阻塞时间。|
