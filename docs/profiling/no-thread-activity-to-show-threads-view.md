---
title: 不显示线程活动（线程视图）| Microsoft Docs
description: 了解“线程”视图，其中当前可见时间范围内没有要显示的活动。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.nothreadreport
helpviewer_keywords:
- Concurrency Visualizer, No Thread Activity to Show (Threads View)
ms.assetid: aa5ae9d0-561d-4ef8-b36b-258ce553d50a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: dcc4cd3241c4d2fffdf2637790869dfc5ac524f5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99922433"
---
# <a name="no-thread-activity-to-show-threads-view"></a>没有要显示的线程活动（线程视图）
此区域显示有关当前可见时间范围内的非隐藏线程的数据。

 如果信息不可见，请检查以下设置：

- 缩放级别太高？ 尝试缩小或滚动，以在范围内显示更多线程活动。

- 是否隐藏太多线程？ 如果是这样，请尝试显示所有线程

- 如果选择了“仅我的代码”，则只能查看有关你的代码的数据。 尝试清除设置以确定是否有任何系统线程活动。

- 确保“降噪”设置为低阈值。

## <a name="see-also"></a>请参阅
- [线程视图](../profiling/threads-view-parallel-performance.md)