---
title: 分析 .NET Core 项目的数据库使用情况 | Microsoft Docs
description: 使用数据库工具记录应用的数据库查询，然后分析这些查询来找到提高性能的方法。
ms.custom: SEO-VS-2020
ms.date: 5/5/2020
ms.topic: conceptual
helpviewer_keywords:
- database, profiling
author: esteban-herrera
ms.author: esherrer
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 758fad160bad89b5e8a4305bf4757302b05732e1
ms.sourcegitcommit: 42aec4a2ea6dec67dbe4c93bcf0fa1116a4b93d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2021
ms.locfileid: "122981081"
---
# <a name="analyze-database-performance-using-the-database-tool"></a>使用数据库工具分析数据库性能

使用数据库工具记录应用在诊断会话期间所进行的数据库查询。 然后，你可以分析各个查询的相关信息，以找到应用性能可改进的地方。

> [!NOTE]
> 数据库工具需要 Visual Studio 2019 版本 16.3 或更高版本，以及使用 [ADO.NET](/dotnet/framework/data/adonet/ado-net-overview) 或 [Entity Framework Core](/ef/core/) 的 Windows 上的 .NET Core 项目。

## <a name="setup"></a>安装

1. 在 Visual Studio 中选择“Alt+F2”打开性能探查器。

1. 选中“数据库”复选框。

   ![数据库工具已选中](./media/db-launch.png "数据库工具已选中")

   > [!NOTE]
   > 如果无法选择该工具，请清除所有其他工具的复选框，因为某些工具需要单独运行。 若要详细了解如何一起运行工具，请参阅[通过命令行使用分析工具](../profiling/using-the-profiling-tools-from-the-command-line.md)。
   >
   > 如果该工具仍不可用，请检查项目是否满足前面的要求。 请确保项目处于“发布”模式，以便捕获最准确的数据。

1. 选择“开始”按钮以运行该工具。

1. 在此工具开始运行后，在应用中完成要探查的方案。 然后选择“停止收集”或关闭应用以查看数据。

1. 收集停止后，会看到一个表，其中显示了在分析会话期间运行的查询。

   ![数据库工具已停止](./media/db-after.png "数据库工具已停止")

查询按时间顺序组织，但你可以按任何列对它们进行排序。 可以通过右键单击列标题来显示更多列。 选择“持续时间”列会使查询按最长持续时间到最短持续时间的顺序排序。

找到要调查的查询后，右键单击该查询。 然后选择“转到源文件”，查看负责该查询的代码。

![“转到源文件”已选中](./media/db-gotosource.png "“转到源文件”已选中")

如果在关系图上选择了时间范围，则查询表仅显示在该时间范围内发生的查询。 如果还运行 [CPU 使用情况工具](./cpu-usage.md?view=vs-2019&preserve-view=true)，此行为将特别有用。

## <a name="see-also"></a>请参阅

- [优化探查器设置](../profiling/optimize-profiler-settings.md)