---
title: 从命令行分析 ASP.NET Web 应用程序 | Microsoft Docs
description: 了解如何从命令行使用分析工具收集 ASP.NET Web 应用程序的性能数据。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling ASP.NET applications
- profling tools,ASP.NET applications
ms.assetid: 897c00d5-5767-433b-a960-4a29c6023ede
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: c4c95890ae4022b854b76d2e4857fc2a27ce97e5
ms.sourcegitcommit: 7a5c4f60667b5792f876953d55192b49a73f5fe9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2021
ms.locfileid: "98533688"
---
# <a name="command-line-profiling-of-aspnet-web-applications"></a>通过命令行分析 ASP.NET Web 应用程序
本部分介绍从命令行使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具收集 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序的性能数据的过程和选项。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

## <a name="common-tasks"></a>常见任务

| 任务 | 相关内容 |
| - | - |
| **轻松收集基本的 ASP.NET 分析数据：** 使用 **VSPerfASPNETCmd** 工具收集采样、检测、.NET 内存、争用或不具有配置要求的层交互数据，以及 **VSPerfCmd** 所需的 Internet 信息服务 (IIS) 重启。 **VSPerfASPNETCmd** 不允许收集额外数据或控制数据收集。 **注意：** VSPerfASPNETCmd 是使用独立探查器分析 ASP.NET 网站的首选工具。 | -   [使用 VSPerfASPNETCmd 进行快速网站分析](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md) |
| **收集应用程序统计信息：** 使用采样法收集性能统计信息。 采样数据适用于分析 CPU 使用率问题以及了解应用程序的常规性能特征。 | -   [使用采样收集应用程序统计信息](../profiling/collecting-application-statistics-for-aspnet-using-the-profiler-sampling-method.md) |
| **收集详细计时数据：** 使用检测方法收集详细计时信息。 检测数据可用于分析 IO 问题和精细分析应用程序方案。 | -   [使用检测收集详细计时数据](../profiling/collecting-detailed-timing-data-aspnet-profiler-instrumentation-method.md) |
| **收集 .NET 内存数据：** 使用采样法或检测法收集显示分配对象的大小和数量的 .NET 内存分配数据。 还可以收集对象生存期数据，此数据显示在每次垃圾回收生成中回收的对象的大小和数量。 | -   [收集内存数据](../profiling/collecting-memory-data-from-an-aspnet-web-application.md) |
| **收集并发数据：** 使用并发方法收集资源争用数据。 **注意：** Web 应用程序不支持收集线程活动和可视化数据。 | -   [收集并发数据](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md) |
| **添加层交互数据：** 可添加 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序对 Microsoft [!INCLUDE[ssNoVersion](../data-tools/includes/ssnoversion_md.md)] 数据库进行的同步 [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)] 调用的相关性能数据。 | -   [收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md) |

## <a name="related-tasks"></a>相关任务

|任务|相关内容|
|----------|---------------------|
|**分析独立（客户端）应用程序**|-   [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)|
|**分析服务**|-   [分析服务](../profiling/command-line-profiling-of-services.md)|
