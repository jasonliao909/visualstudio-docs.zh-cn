---
title: .NET 内存“分配”视图 | Microsoft Docs
description: 了解 .NET 内存分配视图，该视图列出在分析运行期间创建的类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.allocation
helpviewer_keywords:
- performance reports, allocation view
- Allocations view
- profiling tools, Allocation view
- profiling tools reports, Allocation view
ms.assetid: 01eb876e-c413-4516-977b-4f896929e8a6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: f5c456a90ed949063386593734fa21a7b497e361
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735505"
---
# <a name="net-memory-allocations-view"></a>.NET 内存分配视图
“分配”视图列出在分析运行期间创建的类型。 每个类型都是一个调用树的根节点，该调用树显示导致分配该类型的函数执行路径。

 类型行中的数据显示在分析运行期间创建的该类型对象的总数，以及为该类型对象分配的总字节数。 类型的非独占值和独占值始终相同。

- 非独占值用于在函数及其子函数（由调用树中的父函数调用）的实例中创建的对象。

- 独占值用于父函数调用函数时，函数直接创建的对象。 不包括在子函数中创建的对象。

  函数的数据显示创建的对象数，以及为父类型对象分配的字节数。

## <a name="highlight-the-execution-hot-path"></a>突出显示执行热路径
 可以找到调用树中创建了最多父类型对象的执行路径。

- 若要显示最活跃的路径，请右键单击类型或函数，再单击“展开热路径”。

|列|说明|
|------------|-----------------|
|**名称**|已分配类型或函数的名称。|
|**进程 ID**|分析运行的进程 ID (PID)。|
|**进程名**|进程的名称。|
|**模块名**|类型或函数所在模块的名称。|
|**模块路径**|类型或函数所在模块的路径。|
|**源文件**|类型或函数的定义所在的源文件。|
|**函数行号**|此类型定义或函数在源文件中的起始行号。|
|**级别**|指示数据用于类型还是函数。|
|**非独占分配数**|-   对于函数，是该函数创建的父类型对象的总数。 此数目包括在子函数中创建的对象。<br />-   对于类型，是所创建的该类型实例的总数。|
|**非独占分配数百分比**|-   对于函数，是在分析运行期间，该函数创建的所有父类型非独占分配对象的百分比。<br />-   对于类型，是在分析运行期间，所创建的该类型实例对象的总数的百分比。|
|**独占分配数**|-   对于函数，在调用堆栈顶部直接执行函数时创建的对象数。 此数目不包括子函数中创建的对象。<br />-   对于类型，是所创建的该类型实例的总数。|
|**独占分配数百分比**|-   对于函数，是在分析运行期间，该函数创建的所有父类型独占分配对象的百分比。<br />-   对于类型，是在分析运行期间，所创建的该类型实例对象的总数的百分比。|
|**非独占字节数**|-   对于函数，是该函数为父类型对象分配的内存字节数。 此数目包括由其子函数分配的内存。<br />-   对于类型，是在分析运行期间，为该类型实例分配的总字节数。|
|**非独占字节数百分比**|-   对于函数，是在分析运行期间，该函数分配的所有父类型非独占分配内存的百分比。<br />-   对于类型，是在分析运行期间，为该类型实例分配的所有内存的百分比。|
|**独占字节数**|-   对于函数，是该函数为父类型对象分配的内存字节数。 此数目不包括由其子函数分配的内存。<br />-   对于类型，是在分析运行期间，为该类型实例分配的总字节数。|
|**独占字节数百分比**|-   对于函数，是在分析运行期间，该函数分配的所有父类型独占分配内存的百分比。<br />-   对于类型，是在分析运行期间，为该类型实例分配的所有内存的百分比。|
