---
title: 分析性能探查器中的内存使用情况
description: 了解如何使用 Visual Studio 性能探查器中不含调试器的“内存使用情况”工具来监视应用的内存使用情况。
ms.custom: devdivchpfy22
ms.date: 02/18/2022
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 7107648de1810d9b661a42f242a9dba2792a1cbf
ms.sourcegitcommit: 2a3dc3ea8584c0e500c87c2c367a4719455b8dee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2022
ms.locfileid: "139128982"
---
# <a name="analyze-memory-usage-without-debugging-in-the-performance-profiler-c-visual-basic-c-f"></a>在 C#、Visual Basic、C++、F# 性能探查器 (中分析内存使用情况，而无需) 

“内存使用情况”工具监视应用的内存使用情况。 可以使用该工具来研究在 Visual Studio 中正在积极开发的场景的实时内存效果。 可以获取应用内存状态的详细情况快照，并比较快照以找出内存问题的根本原因。 “内存使用”工具支持在 .NET、ASP.NET、C++ 或混合模式（.NET 和本机）应用上使用。

“内存使用情况”工具在[带或不带调试器](../profiling/running-profiling-tools-with-or-without-the-debugger.md)的情况下都可以运行。 本文介绍了如何使用 Visual Studio 性能探查器中不含调试器的内存使用工具，这是推荐用于“发布”版本的工具。 有关根据需求选择最佳内存分析工具的信息，请参阅 [选择内存分析工具](../profiling/memory-usage.md)。

## <a name="memory-usage-diagnostic-sessions"></a>内存使用情况诊断会话

**启动内存使用情况诊断对话：**

1. 在 Visual Studio 中打开项目。

   “内存使用”工具支持 .NET、ASP.NET、C++ 或混合模式（.NET 和本机）应用。

1. 在“调试”菜单中，将解决方案配置设置为“发布”，然后选择“本地 Windows 调试器”（或“本地计算机”）作为部署目标  。

1. 在菜单栏上，**选择"** 调试 > **性能探查器**" 。

1. 在“可用工具”下，选择“内存使用情况”，然后选择“启动”  。

   ![启动内存使用量诊断会话](../profiling/media/memory-usage-start-diagnostics-session.png "启动内存使用量诊断会话")

### <a name="monitor-memory-use"></a>监视内存使用情况

启动诊断会话时，应用将启动，并且“诊断工具”窗口将显示此应用的内存使用情况的时间线图。

::: moniker range="<=vs-2019"
![Visual Studio 性能探查器中“诊断工具”窗口的屏幕截图，其中显示应用内存使用情况的时间线图。](../profiling/media/memory-usage-report-overview.png "内存报告概述")
::: moniker-end

::: moniker range="vs-2022"
![Visual Studio 性能探查器中“诊断工具”窗口的屏幕截图，其中显示应用内存使用情况的时间线图。](../profiling/media/memory-usage-report-overview-vs-2022.png "内存使用情况报表概述")
::: moniker-end

时间线图显示应用运行时的内存波动情况。 该关系图中的峰值通常表明一些代码正在收集或创建数据，然后在处理完成后放弃它。 较大的峰值指示可以优化的区域。 主要关注是内存消耗增加，未返回。 这可能表示内存使用效率低下，甚至内存泄漏。

### <a name="take-snapshots-of-app-memory-states"></a>拍摄应用内存状态的快照

应用使用大量对象，因此你可能希望集中分析某一种情况。 或者，可能会发现要调查的内存问题。 可以在诊断会话期间拍摄快照以捕获特定时刻的内存使用情况。 在出现内存问题之前，获取应用的基线快照是一个不错的选择。 第一次出现问题后，可以拍摄另一个快照，如果可以重复该方案，还可以创建其他快照。

要收集快照，请在要捕获内存数据时选择“拍摄快照”。

### <a name="close-the-diagnostic-session"></a><a name="BKMK_Close_a_monitoring_session"></a> 关闭诊断会话

若要在不创建报告的情况下监视会话，只需关闭诊断窗口。 要在完成收集或拍摄快照后生成报表，请选择“停止收集”。

![停止收集](../profiling/media/memory-usage-stop-collection.png "停止收集")

## <a name="memory-usage-reports"></a>内存使用情况报表

停止收集数据后，“内存使用情况”工具将停止应用并显示“内存使用情况”概述页 。

::: moniker range="<=vs-2019"
![Visual Studio 性能探查器中“内存使用情况”工具中概述页的屏幕截图，其中显示内存使用情况图和两个快照窗格。](../profiling/media/memory-usage-report-overview-1.png "内存使用量概述页")
::: moniker-end

::: moniker range="vs-2022"
![Visual Studio 性能探查器中“内存使用情况”工具中概述页的屏幕截图，其中显示内存使用情况图和两个快照窗格。](../profiling/media/memory-usage-report-overview-1-vs-2022.png "内存使用量概述页")
::: moniker-end

### <a name="memory-usage-snapshots"></a><a name="BKMK_Memory_Usage_snapshot_views"></a> 内存使用情况快照

"快照 **"窗格中** 的数字显示创建每个快照时内存中的对象和字节数，以及快照与上一个快照之间的差值。

这些数字是打开新 Visual Studio 窗口中详细的“内存使用情况”报表视图的链接。 [快照详细报表](#snapshot-details-reports)显示了某个快照中的类型和实例。 [快照差异报表](#snapshot-difference-diff-reports)会比较两个快照中的类型和实例。

::: moniker range="<=vs-2019"
  ![快照视图链接](../profiling/media/memory-usage-snapshot-view-numbered.png "快照视图链接")

|图像|描述|
|-|-|
|![步骤 1](../profiling/media/process-guide-1.png "流程指南-1")|拍摄快照时内存中的字节总数。 选择此链接以显示快照详细信息报表，该报表按类型实例的总大小进行排序。|
|![步骤 2](../profiling/media/process-guide-2.png "流程指南-2")|拍摄快照时内存中的对象总数。 选择此链接以显示快照详细信息报表，该报表按类型实例的计数进行排序。|
|![步骤 3](../profiling/media/process-guide-3.png "流程指南-3")|此快照中内存对象的总大小与前一个快照之间的差异。 正数表示此快照的内存大于前一个快照，负数表示该快照的内存小于前一个快照。 “基线”表示快照是诊断会话中的第一个快照。 “无差异”表示差异为零。 选择此链接以显示快照差异报表，该报表按类型实例的总大小的差异进行排序。|
|![步骤 4](../profiling/media/process-guide-4.png "流程指南-4")|此快照中内存对象的总数与前一个快照之间的差异。 选择此链接以显示快照差异报表。 它按类型实例总数中的差值进行排序。|
::: moniker-end

::: moniker range="vs-2022"
  ![快照视图链接](../profiling/media/memory-usage-snapshot-view-numbered-vs-2022.png "快照视图链接")

|图像|描述|
|-|-|
|![步骤 1](../profiling/media/process-guide-1.png "流程指南-1")|拍摄快照时内存中的对象总数。 选择此链接以显示快照详细信息报表，该报表按类型实例的计数进行排序。|
|![步骤 2](../profiling/media/process-guide-2.png "流程指南-2")|此快照中内存对象的总数与前一个快照之间的差异。 选择此链接以显示快照差异报表，该报表按类型实例总数的差异进行排序。|
|![步骤 3](../profiling/media/process-guide-3.png "流程指南-3")|拍摄快照时内存中的总字节数。选择此链接可显示按类型实例的总大小排序的快照详细信息报表。|
|![步骤 4](../profiling/media/process-guide-4.png "流程指南-4")|此快照中内存对象的总大小与前一个快照之间的差异。 正数表示此快照的内存大于前一个快照，负数表示该快照的内存小于前一个快照。 “基线”表示快照是诊断会话中的第一个快照。 “无差异”表示差异为零。 选择此链接以显示快照差异报表，该报表按类型实例的总大小的差异进行排序。|
::: moniker-end

## <a name="memory-usage-snapshot-reports"></a>内存使用情况快照报表

<a name="BKMK_Snapshot_report_trees"></a> 当在“内存使用情况”概述页中选择某个快照链接时，快照报表将在新页面中打开。

::: moniker range="<=vs-2019"
![“内存使用量”快照报表](../profiling/media/memory-usage-snapshot-report-all.png "“内存使用量”快照报表")
::: moniker-end

::: moniker range="vs-2022"
![“内存使用量”快照报表](../profiling/media/memory-usage-snapshot-report-all-vs-2022.png "“内存使用量”快照报表")
::: moniker-end

如果“对象类型”是蓝色，则可以在单独的窗口中选择它以导航到源代码中的对象。

无法识别或无法理解的代码中涉及的类型可能是 .NET、操作系统或编译器对象。 如果这些对象涉及对象的所有权链，则“内存使用情况”工具会显示这些对象。

在快照报表中：

- " **托管内存** "树显示报告中的类型和实例。 通过选择类型或实例，可以显示选定项的 **根路径** 和 **引用的对象** 树。

- “根的路径”树显示引用类型或实例的对象链。 .NET 垃圾回收器仅在释放对某个对象的所有引用后清理该对象的内存。

- “引用类型”或“引用对象”树显示所选类型或实例引用的对象 。

### <a name="report-tree-filters"></a><a name="BKMK_Report_tree_filters_"></a>报告树筛选器

应用开发人员不需要应用中的许多类型。 快照报表筛选器可以在托管内存和根路径树中隐藏 **大多数** 这些类型。

::: moniker range="<=vs-2019"
![对选项进行排序和筛选](../profiling/media/memory-usage-sort-and-filter.png "内存使用情况排序和筛选")
::: moniker-end

::: moniker range="vs-2022"
![对选项进行排序和筛选](../profiling/media/memory-usage-sort-and-filter-vs-2022.png "内存使用情况排序和筛选")
::: moniker-end

- <a name="BKMK_Filter"></a> 要按类型名称筛选树，请在“筛选器”框中输入名称。 筛选器不区分大小写，并且可识别类型名称任意部分中指定的字符串。

- <a name="BKMK_Collapse_Small_Objects"></a> 在“筛选器”下拉列表中选择“隐藏小型对象”以隐藏以隐藏其大小（字节）小于内存总数 0.5% 的类型  。

- <a name="BKMK_Just_My_Code"></a> 在“筛选器”下拉列表中选择“仅我的代码”，以隐藏由外部代码生成的大多数实例 。 外部类型属于操作系统或 Framework 组件，或者由编译器生成。

## <a name="snapshot-details-reports"></a>快照详细信息报告

 快照详细信息报表描述诊断会话中的一个快照。 要打开此报表，请选择快照窗格中的大小或对象链接。

::: moniker range="<=vs-2019"
 ![快照窗格中指向快照报表的链接](../profiling/media/memory-usage-snapshot-view-snapshot-details-links.png "快照窗格中指向快照报表的链接")
::: moniker-end

::: moniker range="vs-2022"
 ![快照窗格中指向快照报表的链接](../profiling/media/memory-usage-snapshot-view-snapshot-details-links-vs-2022.png "快照窗格中指向快照报表的链接")
::: moniker-end

这两个链接都会打开同一个报表。 唯一的区别是托管内存树的开始 **排序** 顺序。 大小链接按“非独占大小(字节)”列对报表进行排序。 对象链接按“计数”列对报表进行排序。 可以在报表打开后更改排序列或顺序。

### <a name="managed-memory-tree-snapshot-details-reports"></a><a name="BKMK_Managed_Memory_tree__Snapshot_details_"></a> 托管内存树 (快照详细信息报表) 

 托管 **内存** 树列出内存中包含的对象的类型。 展开类型名称以查看类型的最大 10 个实例（按大小排序）。 通过选择类型或实例，以显示选定项的“根的路径”和“引用对象”树 。

::: moniker range="<=vs-2019"
 ![托管堆树](../profiling/media/memory-usage-snapshot-details-managed-heap-tree.png "托管堆树")
::: moniker-end

::: moniker range="vs-2022"
 ![托管内存树](../profiling/media/memory-usage-snapshot-details-managed-heap-tree-vs-2022.png "托管内存树")
::: moniker-end

快照 **详细信息** 报告中的托管内存树具有以下列：

|“属性”|描述|
|-|-|
|“对象类型”|类型或对象实例的名称。|
|“计数”|类型的对象实例数。 对于实例，“计数”始终为 1。|
|“大小(字节)”|对于类型，快照中类型的所有实例的大小小于实例中包含的对象的大小。对于 实例，对象的大小小于 实例中包含的对象的大小。 |
|“非独占大小(字节)”|类型实例的大小或单个实例的大小，其中包括所含对象的大小。|
|**模块**|包含此对象的模块。|

### <a name="paths-to-root-tree-snapshot-details-reports"></a><a name="BKMK_Paths_to_Root_tree__Snapshot_details_"></a> 根的路径树（快照详细信息报表）

“根的路径”树显示引用类型或实例的对象链。 .NET 垃圾回收器仅在释放对某个对象的所有引用后清理该对象的内存。

对于“根的路径”树中的类型，持有对该类型的引用的对象的数量将出现在“引用计数”列中 。

::: moniker range="<=vs-2019"
![类型的根树的路径](../profiling/media/memory-usage-snapshot-details-type-paths-to-root-tree.png "类型的根树的路径")
::: moniker-end

::: moniker range="vs-2022"
![类型的根树的路径](../profiling/media/memory-usage-snapshot-details-type-paths-to-root-tree-vs-2022.png "类型的根树的路径")
::: moniker-end

### <a name="referenced-types-or-referenced-objects-tree-snapshot-details-reports"></a><a name="BKMK_Referenced_Objects_tree__Snapshot_details_"></a> 引用类型或引用对象树（快照详细信息报表）

“引用类型”或“引用对象”树显示所选类型或实例引用的对象 。

::: moniker range="<=vs-2019"
![实例的引用对象树](../profiling/media/memory-usage-snapshot-details-referenced-objects-instance.png "实例的引用对象树")
::: moniker-end

::: moniker range="vs-2022"
![实例的引用对象树](../profiling/media/memory-usage-snapshot-details-referenced-objects-instance-vs-2022.png "实例的引用对象树")
::: moniker-end

“引用类型”树在快照详细信息报表中包含以下列： 引用 **的对象树** 没有"引用 **计数"** 列。

|“属性”|描述|
|-|-|
|“对象类型”或“实例” |类型或实例的名称。|
|**引用计数**|对于类型，该类型的对象实例数。|
|“大小(字节)”|对于类型，类型的所有实例的大小都小于类型中包含的对象的大小。 例如，对象的大小小于对象中包含的对象的大小。|
|“非独占大小(字节)”|类型实例的总大小或实例的大小，其中包括所包含的对象的大小。|
|**模块**|包含此对象的模块。|

## <a name="snapshot-difference-diff-reports"></a>快照差异报告

快照差异（差异）报表显示主快照和前一个快照之间的更改。 要打开差异报表，请在快照窗格中选择差异链接。

这两个链接都会打开同一个报表。 唯一的区别是报告中 **托管内存树** 的开始排序顺序。 大小链接按“非独占大小差异(字节)”列对报表进行排序。 对象链接按“计数差异”列对报表进行排序。 可以在报表打开后更改排序列或顺序。

::: moniker range="<=vs-2019"
 ![快照窗格中指向差异报表的链接](../profiling/media/memory-usage-snapshot-view-snapshot-diff-links.png "快照窗格中指向差异报表的链接")
::: moniker-end

::: moniker range="vs-2022"
 ![快照窗格中指向差异报表的链接](../profiling/media/memory-usage-snapshot-view-snapshot-diff-links-vs-2022.png "快照窗格中指向差异报表的链接")
::: moniker-end

### <a name="managed-memory-tree-snapshot-diff-reports"></a><a name="BKMK_Managed_Memory_tree__Snapshot_diff_"></a> 托管内存树 (快照差异报告) 

 托管 **内存** 树列出内存中包含的对象的类型。 可以展开类型名称以查看类型的最大 10 个实例（按大小排序）。 通过选择类型或实例，以显示选定项的“根的路径”和“引用对象”树 。

::: moniker range="<=vs-2019"
 ![差异报表中类型的托管堆树](../profiling/media/memory-usage-snapshot-diff-type-heap.png "差异报表中类型的托管堆树")
::: moniker-end

::: moniker range="vs-2022"
 ![差异报告中类型的托管内存树](../profiling/media/memory-usage-snapshot-diff-type-heap-vs-2022.png "差异报告中类型的托管内存树")
::: moniker-end

快照 **差异** 报告中的托管内存树具有以下列：

|“属性”|描述|
|-|-|
|“对象类型”|类型或对象实例的名称。|
|“计数”|主要快照中的类型实例的数量。 对于实例，“计数”始终为 1。|
|“计数差异”|对于类型，则为主要快照与上一个快照之间的类型实例数的差异。 对于实例，字段是空白的。|
|“大小(字节)”|主快照中对象的大小小于对象中包含的对象的大小。 对于类型，“大小(字节)”和“非独占大小(字节)”为类型实例的总大小。|
|“总大小差异(字节)”|对于类型，主快照和上一个快照之间的类型实例总大小的差异小于实例中包含的对象的大小。 对于实例，字段是空白的。|
|“非独占大小(字节)”|主要快照中对象的大小，其中包括对象中包含的对象的大小。|
|“非独占大小差异(字节)”|对于类型，主快照和上一个快照之间的所有类型实例大小的差异，其中包括对象中包含的对象的大小。 对于实例，字段是空白的。|
|**模块**|包含此对象的模块。|

### <a name="paths-to-root-tree-snapshot-diff-reports"></a><a name="BKMK_Paths_to_Root_tree__Snapshot_diff_"></a> 根的路径树（快照差异报表）

“根的路径”树显示引用类型或实例的对象链。 .NET 垃圾回收器仅在释放对某个对象的所有引用后清理该对象的内存。

对于“根的路径”树中的类型，持有对该类型的引用的对象的数量将出现在“引用计数”列中 。 上一个快照的差异计数显示在“引用差异”列。

::: moniker range="<=vs-2019"
 ![差异报表中指向根树的路径](../profiling/media/memory-usage-snapshot-diff-paths-to-root-instance-all.png "差异报表中指向根树的路径")
::: moniker-end

::: moniker range="vs-2022"
 ![差异报表中指向根树的路径](../profiling/media/memory-usage-snapshot-diff-paths-to-root-instance-all-vs-2022.png "差异报表中指向根树的路径")
::: moniker-end

### <a name="referenced-types-or-referenced-objects-tree-snapshot-diff-reports"></a><a name="BKMK_Referenced_Objects_tree__Snapshot_diff_"></a> 引用类型或引用对象树（快照差异报表）

“引用类型”或“引用对象”树显示所选类型或实例引用的对象 。

::: moniker range="<=vs-2019"
![差异报表中的引用类型](../profiling/media/memory-usage-snapshot-diff-referenced-types.png "差异报表中的引用类型")
::: moniker-end

::: moniker range="vs-2022"
![差异报表中的引用类型](../profiling/media/memory-usage-snapshot-diff-referenced-types-vs-2022.png "差异报表中的引用类型")
::: moniker-end

“引用类型”树在快照差异报表中包含以下列： “引用对象”树有“实例”大小（字节）、非独占大小（字节）和“模块”列    。

|“属性”|描述|
|-|-|
|“对象类型”或“实例” |类型或对象实例的名称。|
|**引用计数**|主要快照中的类型实例的数量。|
|**引用计数差异**|对于类型，则为主要快照与上一个快照之间的类型实例数的差异。|
|“大小(字节)”|主快照中对象的大小小于对象中包含的对象的大小。 对于类型，“大小(字节)”和“非独占大小(字节)”为类型实例的总大小。|
|“总大小差异(字节)”|对于类型，主快照和上一个快照之间的类型实例总大小的差异小于实例中包含的对象的大小。 |
|“非独占大小(字节)”|主要快照中对象的大小，其中包括对象中包含的对象的大小。|
|“非独占大小差异(字节)”|对于类型，主快照和上一个快照之间的所有类型实例大小的差异，其中包括对象中包含的对象的大小。|
|**模块**|包含此对象的模块。|

## <a name="see-also"></a>请参阅

- [JavaScript 内存](../profiling/javascript-memory.md)
- [使用 Visual Studio 分析](../profiling/index.yml)
- [首先了解分析工具](../profiling/profiling-feature-tour.md)
- [使用 C++、C# 和 Visual Basic 的 UWP 应用的性能最佳做法](/previous-versions/windows/apps/hh750313\(v\=win.10\))
- [Diagnosing memory issues with the new Memory Usage Tool in Visual Studio](https://devblogs.microsoft.com/devops/diagnosing-memory-issues-with-the-new-memory-usage-tool-in-visual-studio/)（在 Visual Studio 中使用新的内存使用情况工具诊断内存问题）
