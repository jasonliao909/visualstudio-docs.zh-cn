---
title: 内核视图时间线 | Microsoft Docs
description: 了解时间线的基础知识：如何确定哪个线程在任何时间点运行哪个内核，以及如何放大和缩小。
custom.ms: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.cores.timeline.threads
helpviewer_keywords:
- Concurrency Visualizer, Cores View Timeline
ms.assetid: 10f0c666-ac2f-4ac5-9fb5-a88f660ab840
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 64012be03c08f3737f4e57a05217bf46082daeb6
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2021
ms.locfileid: "98720743"
---
# <a name="cores-view-timeline"></a>内核视图时间线
时间线中的每一行表示已配置的系统上的一个逻辑处理器内核。 对于每一行，水平轴显示在给定时刻逻辑内核上运行的线程。 将鼠标悬停在时间线上感兴趣的颜色上可返回用于标识线程的工具提示。 为了帮助进行线程标识，窗口底部的图例显示每个颜色所代表的线程。 通过单击并拖动，或通过按住 Ctrl 并移动鼠标滚轮，使用缩放工具进行放大和缩小。 在内核视图与线程视图之间切换时，可保持缩放一致性。

## <a name="see-also"></a>另请参阅
- [内核视图](../profiling/cores-view.md)
- [缩放控件（线程视图）](../profiling/zoom-control-threads-view.md)