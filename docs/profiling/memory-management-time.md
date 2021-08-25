---
title: 内存管理时间 | Microsoft Docs
description: 了解此方案如何意味着线程被与内存管理操作（如分页）关联的事件所阻止。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.paging
helpviewer_keywords:
- Concurrency Visualizer, Paging Time
ms.assetid: 67af3509-3a7d-435d-bc37-5262448da915
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: ed5483c89e9435d5bd0712ef562e80fde2c73e26
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122054530"
---
# <a name="memory-management-time"></a>内存管理时间
时间线中的这些段与归类为内存管理的阻塞时间关联。 此方案意味着线程被与内存管理操作（如分页）关联的事件所阻止。 在此时间内，线程被阻止在并发可视化工具视为内存管理的 API 或内核状态下。 这些包括诸如分页和内存分配这类事件。

 检查关联的调用堆栈和分析报告，以便更好地了解归类为内存管理的阻塞的基本原因。

## <a name="see-also"></a>请参阅
- [线程视图](../profiling/threads-view-parallel-performance.md)