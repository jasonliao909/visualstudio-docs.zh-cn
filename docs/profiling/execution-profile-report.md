---
title: 执行分析报告 | Microsoft Docs
description: 了解执行分析报告，这是 Visual Studio 的并发可视化扩展中的传统采样分析。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.report.execution
helpviewer_keywords:
- Concurrency Visualizer, Execution Profile Report
ms.assetid: c8128472-a8ed-46f4-b1c8-a25358d6f2c1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: d62eac1bb37e297f9247241e4aac073e2406fdcc
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122061059"
---
# <a name="execution-profile-report"></a>执行分析报告
执行分析报告是传统的采样分析。 线程在逻辑内核上运行期间内，将大约每毫秒进行一次采样，并且并发可视化工具可通过调用累积的堆栈集构建典型的调用关系树。 此表中的数据可能受到当前时间范围、隐藏线程和可能应用的筛选器的影响：

- 如果选择“仅我的代码”，则仅会显示具有用户代码的堆栈帧和该用户代码下的一个级别。

- 如果设置了降噪值，则将把低于指定频率的排序堆栈筛从报告中筛选出去

  下表显示报告中的列。

|列|描述|
|------------|-----------------|
|名称|调用堆栈每个级别的函数的名称。|
|非独占样本数|为汇总到此调用堆栈树级别的所有堆栈收集的样本总数。 非独占数是此函数的独占样本数和所有子节点的非独占计数器的总和。|
|独占样本|收集的样本总数，其中此函数是最低的调用堆栈。|
|非独占百分比|非独占样本列中显示的总样本百分比。 百分比舍入到两个小数位。|
|独占百分比|独占样本列中显示的总样本百分比。 百分比舍入到两个小数位。|
|详细信息|该函数的完全限定名。 这包括行计数（如果有）。|

 可在[执行时间（“线程”视图）](../profiling/execution-time-threads-view.md)视图中查看此报告表格。

## <a name="see-also"></a>请参阅
- [线程视图](../profiling/threads-view-parallel-performance.md)