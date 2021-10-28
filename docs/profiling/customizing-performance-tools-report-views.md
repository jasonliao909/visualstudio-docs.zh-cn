---
title: 自定义性能工具报告视图 | Microsoft Docs
description: 查看本部分，了解自定义使用 Visual Studio 分析工具生成的报告的方法。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, customizing report views
- reports, customizing profiling report views
ms.assetid: 5224ac52-0fc2-4269-8eb2-ead7fda3afd4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 46d91c15fb43a735856e537fe09c94ba33aa439a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641722"
---
# <a name="customize-performance-tools-report-views"></a>自定义性能工具报告视图
本节介绍如何自定义使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具生成的报告。

## <a name="common-tasks"></a>常见任务

|任务|相关内容|
|----------|---------------------|
|**在报告视图中对列进行添加、删除和排序：** 可以指定要在基于表的视图中显示的列，并可以指定列的显示顺序。 还可以按列值对报告表的行进行排序。|-   [如何：自定义报表视图列](../profiling/how-to-customize-report-view-columns.md)|
|**从报告中消除小型函数：** 可以从报告中消除小于指定阈值的函数。|-   [如何：在报表视图中配置降噪](../profiling/how-to-configure-noise-reduction-in-report-views.md)|
|**筛选报告视图中的数据**：可以将报告中显示的数据限制为分析运行的某个时间段。 可以在“摘要”视图的时间线图中指定时间段，也可以在报告视图筛选器中定义的查询中指定时间段。 还可以筛选报告，使其仅显示代码文件中定义的函数。|-   [筛选报告视图](../profiling/filtering-report-views.md)<br />-   [如何：从摘要时间线中筛选报表视图](../profiling/how-to-filter-report-views-from-the-summary-timeline.md)<br />-   [如何：筛选分析工具报表视图以显示“仅我的代码”](../profiling/how-to-filter-profiling-tools-report-views-to-display-just-my-code.md)<br />-   [性能报告视图筛选器](../profiling/performance-report-view-filter.md)|

## <a name="related-sections"></a>相关章节
- [“性能报表”视图](../profiling/performance-report-views.md)介绍可用于对分析数据进行分析的视图。

## <a name="see-also"></a>另请参阅
- [分析性能工具数据](../profiling/analyzing-performance-tools-data.md)
