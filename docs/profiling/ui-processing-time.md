---
title: UI 处理时间 | Microsoft Docs
description: 了解时间线中的时间段与归类为 UI 处理的阻塞时间关联。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.uiprocessing
helpviewer_keywords:
- Concurrency Visualizer, UI Processing Time
ms.assetid: 0ddb05a3-8c6b-448b-8488-2751c1e5abcc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 63462aedfb1d7a2c03fe6ff5d59495358c52194e
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2021
ms.locfileid: "98722381"
---
# <a name="ui-processing-time"></a>UI 处理时间
时间线中的这些时间段与归类为 UI 处理的阻塞时间关联。 这表示有一个线程正在发送 Windows 消息或正在执行其他用户界面 (UI) 操作。 在此时间内，线程已在被并发可视化工具计数为 UI 处理的 API 中阻塞。 `GetMessage()` 和 `MsgWaitForMultipleObjects()` 等 API 就归为此组。

 如果未标识预定义的阻塞 API，请检查调用堆栈和分析报告，确定造成延迟的根本原因。

 UI 处理类别帮助你理解 GUI 应用程序的响应能力，非常适合依赖 UI 响应能力的应用程序。 例如，如果应用程序中的 UI 线程能够将 100% 的时间用于 UI 处理，则该应用程序的响应速度可能会很快。 但是，如果 UI 线程花费了大量时间在其他类别上，则需查找根本原因并考虑降低该线程上的非 UI 类别。

## <a name="see-also"></a>请参阅
- [线程视图](../profiling/threads-view-parallel-performance.md)