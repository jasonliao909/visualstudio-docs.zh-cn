---
title: “行”视图 | Microsoft Docs
description: 了解“行”视图如何仅适用于使用采样方法收集的探查器数据。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.lines
helpviewer_keywords:
- profiling tools reports, Line view
- profiling tools, Line view
- Lines view
ms.assetid: 71ec0781-6031-4e17-af09-f50226018437
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 645bd910ec6213f9aef006f7e95e1f3fe7833250
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736179"
---
# <a name="lines-view"></a>“行”视图
“行”视图仅适用于使用采样方法收集的探查器数据， 不适用于使用检测方法收集的数据。

 对于采样分析数据，“行”视图标识在收集样本时直接执行的函数中的语句。 对于 .NET 内存数据，“行”视图标识分配内存的语句。

 在源文件中，一个语句可以跨多个行，一行可以包含多个语句。

 语句由以下数据标识：

- 包含函数语句的源文件。

- 包含该语句的函数。

- 该语句的起始源代码行。

- 该语句的起始源代码行中的字符。

- 该语句的结束源代码行。

- 该语句的结束源代码行中的字符。

## <a name="see-also"></a>另请参阅
- [“行”视图](../profiling/lines-view-sampling-data.md)
- [“行”视图 - 采样](../profiling/lines-view-dotnet-memory-sampling-data.md)
- [“行”视图](../profiling/lines-view-contention-data.md)
