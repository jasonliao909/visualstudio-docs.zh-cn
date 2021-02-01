---
title: 磁盘操作报告（“线程”视图）| Microsoft Docs
description: 磁盘操作报告显示磁盘通道中的磁盘 I/O 操作。 查看为每个磁盘访问报告的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.report.diskoperations
helpviewer_keywords:
- Concurrency Visualizer, File Operations Report (Threads View)
ms.assetid: e352f4f3-f654-45eb-96ed-417863487ddc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 44975999c71b1c331d90aa10f709071cef466cb1
ms.sourcegitcommit: d13f7050c873b6284911d1f4acf07cfd29360183
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2021
ms.locfileid: "98686527"
---
# <a name="disk-operations-report-threads-view"></a>磁盘操作报告（线程视图）
磁盘操作报告显示磁盘通道中的磁盘 I/O 操作。

 对于代表正在当前可见时间窗口中进行分析的进程而发生的每次磁盘访问，将报告以下信息：

- 执行磁盘访问的进程的名称和 PID

- 访问磁盘的线程的 ID

- 被访问的文件的名称。

- 每个文件的读取数

- 读取的字节数

- 读取延迟时间（以毫秒为单位）

- 写入数

- 写入的字节数

- 写入延迟时间（以毫秒为单位）

## <a name="see-also"></a>请参阅
- [线程视图](../profiling/threads-view-parallel-performance.md)