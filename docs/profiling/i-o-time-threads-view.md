---
title: I-O 时间（“线程”视图）| Microsoft Docs
description: 了解 I/O 时段如何与分类为 I/O 的阻塞时间关联，这意味着线程正在等待完成 I/O 操作。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.io
helpviewer_keywords:
- Concurrency Visualizer, I/O time (Threads View)
ms.assetid: 0c4ec14d-d8dd-49c1-999c-dcbf4e8e1dc8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 915ab6aef595fba7e13321d4e23c08bdd2eadaf3
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2021
ms.locfileid: "98721627"
---
# <a name="io-time-threads-view"></a>I/O 时间（“线程”视图）
时间线中的这些段与归类为 I/O 的阻塞时间关联。 这意味着一个线程正在等待 I/O 操作完成。 此线程可能已在 API 中被阻止，或由将并发可视化工具视为 I/O 的 I/O 相关内核等待阻止。 此组中包括 `CreateFile()`、`ReadFile()` 和 `WSARecv()` 等 API。

## <a name="see-also"></a>请参阅
- [线程视图](../profiling/threads-view-parallel-performance.md)