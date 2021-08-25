---
title: “标记”视图 | Microsoft Docs
description: 了解“标记”视图如何显示插入到应用程序的采样和 ETW 事件。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.marks
helpviewer_keywords:
- profiling tools, Marks view
- profiling tools reports, Marks view
ms.assetid: b2773344-8081-4116-85a1-58f770448f6a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 9cf6b69960980507bebd036ac49332dfa42aed9a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122076433"
---
# <a name="marks-view"></a>“标记”视图
“标记”视图显示插入到应用程序的采样和 ETW 事件。

 在报表中预先填充的默认标记可用来标记程序开始和程序结束。

 来自自动生成的标记的 Windows 计数器数据也显示在此视图中。 有关详细信息，请参阅[如何：收集 Windows 计数器数据](../profiling/how-to-collect-windows-counter-data.md)。

 若要创建两个标记之间的筛选器，请选择标记，右键单击，然后单击“添加筛选器(按标记)”或“添加筛选器(按时间戳)”。

 下表提供了“标记”视图中可用列的定义。

 **标记 ID** 分析标记的唯一标识符。

 **标记名称** 事件的名称。

 **时间戳** 从开始分析到记录事件的时间。

 Windows 性能计数器数据 收集 Windows 性能计数器数据时，值将显示在具有该计数器名称的列中。

## <a name="see-also"></a>另请参阅
- [性能报告概述](../profiling/performance-report-overview.md)
- [如何：收集 Windows 计数器数据](../profiling/how-to-collect-windows-counter-data.md)
- [[NIB] 数据收集控件窗口](/previous-versions/bb385767(v=vs.110))