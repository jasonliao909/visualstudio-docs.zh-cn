---
title: 创建探查器比较报告（命令行）
description: 使用命令行中的 VSPerfReport.exe 比较两个探查器数据文件的结果。 此比较显示了分析会话之间的差异。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 00548d16-eb5b-46f7-8a65-862f98a43831
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: ffa80280a5dda1d8fc25e40c8ed5269d3328a5ab
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122150243"
---
# <a name="how-to-create-a-profiler-comparison-report-from-a-command-prompt"></a>如何：通过命令提示符创建探查器比较报告
可生成 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具报告，用于比较两个分析数据文件（.vsp 或 .vsps）的性能数据 。 报告显示从一个分析会话到另一个分析会话所发生的差异、性能回归和改进。 报告中的值表示基于指定的首个文件的基线的增量（或变化）。 此增量是通过确定旧值（基准值）与新分析所得结果值之差计算而得。 探查器数据的比较可基于代码中的函数、应用程序中的模块、行、指令指针 (IP) 和类型。

 若要列出比较类别和字段的标识符，请键入以下命令行：

 **VSPerfReport /querydifftables**  *VspFileName1* *VspFileName2*

 使用以下语法创建比较报告：

 **VSPerfReport /diff**  `VspFileName1` *VspFileName2* [ **/** `Options`]

 可以向 VSPerfReport /diff 命令行添加下表中的选项。

|选项|描述|
|------------|-----------------|
|DiffThreshold:[Value]|如果差异低于此百分比阀值，则忽略该差异。 此外，不会显示值低于此阈值的新数据。|
|**DiffTable：** *TableName*|使用此表比较文件。 默认使用函数表。 指定 VSPerfReport /querydifftables 中列出的标识符。|
|**DiffColumn：** *ColumnName*|使用此列对值进行比较。 默认情况下，使用独占样本百分比列。 指定 VSPerfReport /querydifftables 中列出的标识符。|
