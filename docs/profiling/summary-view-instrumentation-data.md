---
title: “摘要”视图 - 检测数据 | Microsoft Docs
description: 了解“摘要”视图如何显示有关性能开销最大的函数的信息以及“通知”链接和“报告”列表的说明。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Summary view
ms.assetid: 0a3b3a1f-e22b-4ac8-b46e-71694e9b2cf1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: c5d8579b68eeceed3843a8dd6a6fe71e9f9015c2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122141228"
---
# <a name="summary-view---instrumentation-data"></a>“摘要”视图 - 检测数据
“摘要”视图显示有关分析运行中性能开销最大的函数的信息。 有关详细信息（包括通知链接和报告列表的说明），请参阅[“摘要”视图](../profiling/summary-view.md)。

## <a name="timeline-graph"></a>时间线关系图
 “摘要”视图中的时间线关系图按分析的应用程序显示在进行分析的时间内的处理器 (CPU) 利用率。 可以使用时间线关系图将视图筛选到所选时间范围。 有关详细信息，请参阅[如何：从摘要时间线中筛选报表视图](../profiling/how-to-filter-report-views-from-the-summary-timeline.md)。

## <a name="hot-path"></a>热路径
 “热路径”显示使用最多时间的执行路径。 可以单击某个函数以显示该函数的“函数详细信息”视图。 若要显示函数的其他视图，请右键单击函数，然后单击列表中的视图。

 “热路径”包含每个函数的以下数据：

|列|说明|
|------------|-----------------|
|**名称**|函数的名称。|
|**已用非独占时间百分比**|此函数在其函数体中以及在它调用的函数中执行代码所花的时间占分析数据中所有时间的百分比。|
|**已用独占时间百分比**|此函数在其函数体中执行代码所花的时间占分析数据中所有时间的百分比。 不包含在此函数调用的函数中所花的时间。|

## <a name="functions-with-most-individual-work"></a>大部分时间单独工作的函数
 将大多数时间用于在自己的函数体中而不是在调用的函数中执行代码的函数的列表。

 “大部分时间单独工作的函数”包含每个函数的以下数据：

|列|说明|
|------------|-----------------|
|**名称**|函数的名称。|
|**独占时间百分比**|此函数在其函数体中执行代码所花的时间占分析数据中所有时间的百分比。 不包含在此函数调用的函数中所花的时间。|

## <a name="see-also"></a>请参阅
- [“摘要”视图 - 采样数据](../profiling/summary-view-sampling-data.md)
- [“摘要”视图 - .NET 内存数据](../profiling/summary-view-dotnet-memory-data.md)
