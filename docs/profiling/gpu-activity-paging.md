---
title: GPU 活动(分页) | Microsoft Docs
description: 查看并发可视化工具的“线程”选项卡上的 GPU 活动（分页）段。 这些段表示 GPU 处理分页请求的时间。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.gpuactivity
- vs.cv.threads.timeline.gpupaging
ms.assetid: 95284ac5-3492-4f7b-a79f-7d2840a07679
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2bdf1fcffad90155baba8f92d11e31d1b316710b
ms.sourcegitcommit: 589d96700208bf22c8da9e26a1d2041fbf39b8f9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98801185"
---
# <a name="gpu-activity-paging"></a>GPU 活动(分页)
“线程”选项卡上的“GPU 活动(分页)”段表示 GPU 处理分页请求的时间。  段的长度代表 GPU 处理直接内存访问 (DMA) 数据包时的持续时间。 通常，分页数据包与 CPU 和 GPU 之间的内存转移有关。

 当选择某个 GPU 分页段时，“当前”选项卡上的报告将显示所处理的 DMA 数据包的相关信息。 这包括它在与 DirectX 引擎关联的硬件队列中等待的总时间、提交 DMA 数据包的进程，以及处理数据包所需的时间。

## <a name="see-also"></a>另请参阅
- [使用率视图](../profiling/utilization-view.md)