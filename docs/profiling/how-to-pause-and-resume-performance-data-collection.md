---
title: 暂停和恢复性能数据收集 | Microsoft Docs
description: 了解在分析会话页窗口中，如何交互控制分析数据的收集。
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- profiling tools, remote profiling
ms.assetid: b8e76363-65cd-424d-8173-3e2b5f54203b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 518aa042609b830709d8671a8b0a68156efa6314
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126642317"
---
# <a name="how-to-pause-and-resume-performance-data-collection"></a>如何：暂停和恢复性能数据收集
在分析会话页窗口中，您可以交互控制分析数据的收集。

 通过控制数据收集，可以减小分析数据文件的大小，以及仅收集感兴趣的那些操作的数据。 可以在一个性能会话中多次暂停和恢复分析。

 ![分析会话页](../profiling/media/prof_profilingsessionpage.png "PROF_ProfilingSessionPage")

> [!NOTE]
> 还可以在暂停分析的情况下启动性能会话，然后在以后执行程序时恢复分析。 若要在暂停分析的情况下启动性能会话，请选择“调试”菜单中的“在暂停分析的情况下启动性能分析”命令 。

### <a name="to-pause--resume-or-stop-profiling"></a>暂停、恢复或停止分析

- 在分析会话页上：

  - 选择“暂停收集”可暂停数据收集。

  - 暂停数据收集后，选择“恢复收集”可重新启动数据收集。

  - 选择“停止分析”可结束分析会话并生成报告。

## <a name="see-also"></a>请参阅
- [控制数据收集](../profiling/controlling-data-collection.md)
- [如何：启动和结束性能数据收集](../profiling/how-to-start-and-end-performance-data-collection.md)
