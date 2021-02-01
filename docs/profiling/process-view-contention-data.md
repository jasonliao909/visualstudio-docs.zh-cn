---
title: “进程”视图 - 争用数据 | Microsoft Docs
description: 了解“进程”视图如何显示在分析运行期间执行的进程和线程的争用数据。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Process view
ms.assetid: 8821d98c-0771-43b2-a38b-e9039a3abd75
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: f3eb95c5ba8bb9f519623d4b43bc80d37919305d
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2021
ms.locfileid: "98719461"
---
# <a name="process-view---contention-data"></a>“进程”视图 - 争用数据
“进程”视图显示在分析运行期间执行的进程和线程的争用数据。

 当符号可用时，进程会按名称列出。 当符号不可用时，进程会按其内存地址（十六进制格式）列出。 线程作为创建它们的进程的子级列出。

 下表说明“进程”视图表中各列的值。

|列|说明|
|------------|-----------------|
|**开始时间**|从分析开始到进程或线程启动的毫秒数或处理器周期数。|
|**阻塞的时间**|在此期间阻止进程或线程的函数执行的总时间。|
|**阻塞的时间百分比**|在此期间阻止进程或线程的函数执行的时间占进程或线程生存期的百分比。|
|**争用**|阻止进程或线程的函数执行的次数。|
|**争用数百分比**|进程或线程的争用占分析运行期间所有争用的百分比。|
|**结束时间**|从分析开始到进程或线程结束的毫秒数或处理器周期数。|
|**ID**|进程或线程的系统生成的标识符。|
|**生存时间**|从进程或线程启动到进程或线程结束或分析结束的毫秒数或处理器周期数。|
|**Type**|行的类型（进程或线程）。<br /><br /> 仅在 **VSReport** 命令行报表中。 有关详细信息，请参阅 [VSPerfReport](../profiling/vsperfreport.md)。|
|**名称**|进程或线程的名称。|
|**唯一 ID**|探查器生成的标识符，对进程或线程是唯一的。|

## <a name="see-also"></a>另请参阅
- [如何：自定义报表视图列](../profiling/how-to-customize-report-view-columns.md)
- [“进程”视图](../profiling/process-view.md)
