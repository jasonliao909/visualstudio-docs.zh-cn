---
title: “当前”选项卡 | Microsoft Docs
description: 选择线程视图的“当前”选项卡以查看 CPU 线程段或阻塞段的调用堆栈。 还提供了有关 DirectX 段的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.reportnav.current
helpviewer_keywords:
- Concurrency Visualizer, Callstack at Selection Point
ms.assetid: 2c7b1ae5-3756-4795-bc59-f6bb113f2ba5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 05055cfc315c2b86693ec76e23a448a12679335d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641729"
---
# <a name="current-tab"></a>“当前”选项卡
如果选择一个 CPU 线程段，则通过单击“当前”选项卡，可以查看时间线中最接近当前选择点的调用堆栈（如果有）。  在这种情况下，选择点由时间线上方的黑色箭头或插入符号来表示。 选择阻塞段时，将不显示插入符号，因为没有任何执行操作。 但是，仍会突出显示该段，并显示调用堆栈。

 “当前”选项卡还显示有关 DirectX 活动段、标记和 I/O 访问的信息。  对于 DirectX 活动段，将会显示有关硬件队列如何处理 DMA 数据包的信息。  对于标记，将会显示有关说明和标记类型的信息。  对于 I/O 访问，将会显示有关文件和读取或写入字节数的信息。

## <a name="see-also"></a>请参阅
- [线程视图](../profiling/threads-view-parallel-performance.md)