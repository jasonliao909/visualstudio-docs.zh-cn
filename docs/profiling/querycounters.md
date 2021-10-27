---
title: QueryCounters | Microsoft Docs
description: 了解“QueryCounters”选项如何列出计算机上可用的 CPU（硬件）性能计数器。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 8059d4b2-af61-4a47-a6c2-8da5c0741c74
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: d5dea7b93bded032f51650b895f16ad44948443c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735854"
---
# <a name="querycounters"></a>QueryCounters
“QueryCounters”选项列出计算机上可用的 CPU（硬件）性能计数器。

 “QueryCounters”必须是命令行中的唯一选项。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /QueryCounters
```

#### <a name="parameters"></a>参数
 无

## <a name="remarks"></a>备注
 使用检测方法时，探查器可以在每个数据收集事件中收集一个或多个 CPU 性能计数器的值。 使用采样分析方法时，可以指定一个计数器事件和要用作采样间隔的事件发生数。

 不同的处理器公开不同的 CPU 性能计数器。 探查器定义一组可用于几乎所有处理器的常规计数器。 “QueryCounters”选项同时列出常规计数器的名称和特定于处理器的计数器名称。

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
