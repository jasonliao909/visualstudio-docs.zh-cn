---
title: 分析工具使用规则 | Microsoft Docs
description: 了解分析工具使用类别中的性能规则如何提供有关最有效地使用探查器收集数据的指南。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: afa7db3b-8c1d-473a-81ac-24ede112a17f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 858a49a02e335f169bda60182d5388971cc6f29b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122054543"
---
# <a name="profiling-tools-usage-rules"></a>分析工具使用规则
分析工具使用类别中的性能规则提供有关最有效地使用探查器收集数据的指南。

| 规则 | 描述 |
| - | - |
| [DA0002：缺少 VSPerfCorProf.dll](../profiling/da0002-vsperfcorprof-dll-is-missing.md) | 命令行分析可能包含不完整的 .NET Framework 二进制文件数据。 这可能由未设置正确环境变量所导致。 |
| [DA0003：大量内核样本](../profiling/da0003-many-kernel-samples.md) | 记录了在目标二进制文件执行外部出现的大量分析样本。 若要收集更准确的数据，请考虑使用检测方法。 |
| [DA0004：处理器使用情况很高](../profiling/da0004-high-processor-usage.md) | 分析数据暗示处理器在分析运行期间一直繁忙。 若要收集更准确的数据，请考虑使用采样方法。 |
| [DA0008：收集的样本过少](../profiling/da0008-few-samples-collected.md) | 在分析运行中收集的样本数不足以具有统计意义。 请考虑再次进行分析并较长时间地运行应用程序。 还可以考虑使用检测方法收集数据。 |
| [DA0026：处理过程的内核 CPU 时间过长](../profiling/da0026-excessive-kernel-cpu-time-processing.md) | 分析运行中有大量时间处于处理器内核模式下。 请考虑通过将系统调用用作指标（而不是将时间用作指标）来进行采样。 |
| [DA0029：CLR 版本不受支持](../profiling/da0029-unsupported-clr-version.md) | 分析的二进制文件使用探查器不支持的 .NET Framework 版本。 探查器报告无法解析符号名称。 |
| [DA0030：收集数据库项目的“层交互”度量值](../profiling/da0030-gather-tier-interaction-measurements-for-database-projects.md) | 收集了大量对 <xref:System.Data?displayProperty=fullName> 命名空间中的方法进行的调用。 若要包含有关数据库调用的数据，请考虑在分析运行中收集层交互数据。 |
