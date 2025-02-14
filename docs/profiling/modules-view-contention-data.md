---
title: “模块”视图：争用数据 | Microsoft Docs
description: 了解争用数据的“模块”视图如何显示按分析数据中采样的模块分组的并发数据。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Modules view
ms.assetid: 1a9aa122-2d8f-4a09-b503-92975aa6b648
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 556e7becfd87cd9ffd9a47737cee1330d93413b9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640762"
---
# <a name="modules-view---contention-data"></a>“模块”视图 - 争用数据
争用数据的“模块”视图显示按分析数据中采样的模块分组的并发数据。 每个模块都是一个层次结构树的根。 模块节点下列出其中发生争用事件的模块的函数。

 如果函数在争用事件发生时正在执行自己的代码，即函数位于调用堆栈的顶部，则执行的源行和指令地址会在函数节点下列出。 因为在执行行或指令时会为源行或指令指针收集数据，所以非独占和独占值对于行数据和指令数据始终是相同的。

 下表介绍争用数据的“模块”视图中各列的值。

|列|描述|
|------------|-----------------|
|**独占阻塞的时间**|-   对于函数，为阻塞此函数执行函数体内代码的时间。 不包含此函数调用的函数中的阻塞时间。<br />-   对于模块，为模块中各个函数独占阻塞时间之和。<br />-   对于行或指令，为阻塞此行或指令执行的时间。|
|**独占阻塞的时间百分比**|-   对于函数或模块，为此函数或模块的独占阻塞时间占分析运行期间所有阻塞时间的百分比。<br />-   对于行或指令，为阻塞此行或指令执行的时间占分析运行期间所有阻塞时间的百分比。|
|**独占争用**|-   对于函数，为阻塞此函数执行函数体内代码的次数。 不包含该函数所调用的函数中的争用。<br />-   对于模块，为模块中各个函数的独占争用之和。<br />-   对于行或指令，为阻塞此行或指令执行的次数。|
|**独占争用数百分比**|-   对于函数或模块，为此函数或模块的独占争用占分析运行期间所有争用的百分比。<br />-   对于行或指令，为阻塞此行或指令执行的争用占分析运行期间所有争用的百分比。|
|**非独占阻塞的时间**|-   对于函数，为阻塞此函数或此函数调用的函数执行的时间。<br />-   对于模块，为此模块中至少一个函数位于堆栈上的阻塞时间之和。<br />-   对于行或指令，为阻塞此行或指令执行的时间。|
|**非独占阻塞的时间百分比**|-   对于函数或模块，为此函数或模块的非独占阻塞时间占分析运行期间所有阻塞时间的百分比。<br />-   对于行或指令，为执行此行或指令的时间占分析运行期间所有阻塞时间的百分比。|
|**非独占争用**|-   对于函数，为阻塞此函数或此函数调用的函数执行的次数。<br />-   对于模块，为此模块中至少一个函数位于堆栈上的争用的次数。<br />-   对于行或指令，为阻塞此行或指令执行的次数。|
|**非独占争用数百分比**|-   对于函数或模块，为此函数或模块的非独占争用占分析运行期间所有争用的百分比。<br />-   对于行或指令，为执行此行或指令的时间占分析运行期间所有阻塞时间的百分比。|
|**函数行号**|此函数在源文件中的起始行号。|
|**模块名**|包含函数、行或指令指针的模块的名称。|
|**模块路径**|包含模块、函数、行或指令指针的模块的路径。|
|**名称**|模块或函数的名称。|
|**进程 ID**|分析运行的进程 ID (PID)。|
|**进程名**|进程的名称。|
|**源文件**|此函数的定义所在的源文件。|

## <a name="see-also"></a>请参阅
- [如何：自定义报表视图列](../profiling/how-to-customize-report-view-columns.md)
- [“模块”视图](../profiling/modules-view.md)
- [“模块”视图 - 检测](../profiling/modules-view-dotnet-memory-instrumentation-data.md)
- [“模块”视图 - 采样](../profiling/modules-view-dotnet-memory-sampling-data.md)
- [“模块”视图](../profiling/modules-view-instrumentation-data.md)
- [“模块”视图](../profiling/modules-view-sampling-data.md)
