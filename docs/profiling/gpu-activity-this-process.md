---
title: GPU 活动(此进程) | Microsoft Docs
description: 在并发可视化工具的“线程”视图中阅读有关 GPU 活动（此过程）段的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.gpuexecution
ms.assetid: 0956edbf-9bcd-4afe-9287-fda628648ca0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9c4249ee5992840449771e1acdcf491877199dde
ms.sourcegitcommit: 965372ad0d75f015403c1af508080bf799914ce3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "135803409"
---
# <a name="gpu-activity-this-process"></a>GPU 活动(此进程)
在并发可视化工具中，“线程”视图中的“GPU 活动(此进程)”段表示 GPU 代表当前进程处理请求的时间。 这些请求以直接内存访问 (DMA) 数据包的形式发送到 GPU。 段的长度代表 GPU 代表当前进程处理 DMA 数据包的时间。

 当选择 GPU 活动段时，“当前”选项卡上的报告将显示所处理的 DMA 数据包的相关信息。 此信息包括数据包在与 DirectX 引擎关联的硬件队列中等待的总时间、提交数据包的进程，以及处理数据包所需的时间。 当前进程外的某个进程可能以物理方式将 DMA 数据包提交给了 GPU。 当另一个进程代表当前进程将工作提交给 GPU 时，并发可视化工具可以检测出来。