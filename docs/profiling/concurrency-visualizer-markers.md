---
title: 并发可视化工具标记 | Microsoft Docs
description: 了解并发可视化工具中的标记。 标记图标表示由应用生成的事件。 有三种类型：标志、消息和范围。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.markersui
- vs.cv.markers.flag
- vs.cv.markers.message
- vs.cv.markers.span
ms.assetid: c4692d17-6cd2-4ad1-8590-d7275c771c70
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 2191bc093b97029f446359c435db387291f2c29d
ms.sourcegitcommit: caf5ca17efde4dc4de8b1bdfbe7770f6d705024d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2022
ms.locfileid: "145017720"
---
# <a name="concurrency-visualizer-markers"></a>并发可视化工具标记

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]
在并发可视化工具中，标记是代表应用事件的图标。  通常，应用生成这些事件是为了指定应用程序中的阶段或匹配项。  事件可以由应用或应用所使用的库和运行时生成。

## <a name="kinds-of-markers"></a>标记类型
 并发可视化工具使用三类标记来表示应用程序事件：标志、消息和跨度。

1. *标志* 用于指示应用中关注的时间点。  例如，您可以使用标记来表示一个达到特定阈值或引发异常的变量值。

2. *消息* 也标记时间点，但可以将其用于日志样式的跟踪。  例如，过去可能转储到日志文件的内容，现在可以包装到消息调用中，以便对其进行追踪并在并发可视化工具中查看。 还可以使用并发可视化工具将此数据导出到 CSV 文件。

3. *范围* 表示应用中的时间间隔，例如，它其中的某个阶段。

## <a name="marker-linkage-to-threads"></a>线程的标记链接
 每个生成标记的线程都有单独的时间线通道。  负责生成标记事件的线程的 ID 显示在标记通道的说明旁。  标记通道左侧显示的 ID 与当前进程中其他线程的 ID 匹配。

## <a name="marker-importance"></a>标记重要性
 标记可以有四种重要性级别：低，常规，高和重要。  您可以根据重要性级别筛选标记源。  例如，如果只想查看重要性级别为“常规”或“重要”的特定源的标记，则可以在“[高级设置](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md)”对话框中配置筛选器。 标记重要性显示在其工具提示和[标记报告](../profiling/threads-view-reports.md#markers-report)中。

## <a name="marker-category"></a>标记类别
 标记类别表示来自同一来源的一组标记事件。  并发可视化工具使用颜色来区分不同的标志和跨度类别。 您可以配置并发可视化工具，使之用类别来筛选来自特定事件提供程序的事件标记。  使用[高级设置](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md)对话框以配置筛选器。

## <a name="known-sources-of-markers"></a>已知的标记源
 只要某些约束，任何 ETW 提供程序都可以生成标记。 您可以配置并发可视化工具，使之侦听其他的标记事件源。 默认情况下，它将侦听这些事件源：

- [并发可视化工具 SDK](../profiling/concurrency-visualizer-sdk.md)

- [任务并行库 (TPL)](/dotnet/standard/parallel-programming/task-parallel-library-tpl)

- [数据流](/dotnet/standard/parallel-programming/dataflow-task-parallel-library)

- [并行 LINQ (PLINQ)](/dotnet/standard/parallel-programming/parallel-linq-plinq)

- [并发运行时](/cpp/parallel/concrt/concurrency-runtime)

- [方案标记支持](/previous-versions/visualstudio/visual-studio-2010/dd984115\(v\=vs.100\))

- [C++ AMP (C++ Accelerated Massive Parallelism)](/cpp/parallel/amp/cpp-amp-cpp-accelerated-massive-parallelism)

  使用[高级设置](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md)对话框中的“标记”选项卡，可以控制是否在并发可视化工具中显示来自不同源的标记，也可以根据重要性和类别来筛选标记。

## <a name="markers-from-eventsource"></a>来自 EventSource 的标记
 并发可视化工具还可以显示 EventSource 事件。  有关详细信息，请参阅[将 EventSource 事件作为标记可视化](../profiling/visualizing-eventsource-events-as-markers.md)。

## <a name="flag-markers"></a>标志标记

标志标记表示某一瞬间在应用中发生的事。 标志可以表示许多应用程序事件。 例如，标志可以显示特定工作项的计划时间或引发异常的时间。 诸如任务并行库等运行时也可以生成标志。

### <a name="flag-importance"></a>标志重要性
 标志以不同的大小显示，具体取决于它们的重要性。 与所有标记一样，重要性可以是低、常规、高或重要。  此图按重要性级别显示各标记的外观：

 ![低、普通、高和关键重要性标记的插图。](../profiling/media/cvmarkerimportance.png "CVMarkerImportance")

### <a name="flag-category"></a>标志类别
 标志显示为五种不同的颜色，具体取决于其类别。 如果有 5 个以上的类别，则会重复使用颜色。 不能选择颜色。 与所有标记一样，类别可以是任意整数。 下一个插图显示前 5 个类别的颜色。

 ![类别标记的五种颜色的插图。](../profiling/media/cvmarkercategory.png "CVMarkerCategory")

### <a name="alerts"></a>警报
 警报是一种表示重要应用程序事件（例如，异常）的红色标志。  以下是一个警报：

 ![并发可视化工具警报标记的插图。](../profiling/media/cvmarkeralert.png "CVMarkerAlert")

### <a name="aggregation-flags"></a>聚合标志
 有时，并发可视化工具中标志的发生时间过于接近，导致无法单独绘制。 发生这种情况时，将显示代表基础标志的灰色聚合标志。 当将鼠标指针放在这些图标上时，工具提示将显示所代表的基础标志数量。 若要查看这些标志，请将其放大。 如果一直放大但仍显示聚合标志，则可以在[标记报表](../profiling/threads-view-reports.md#markers-report)中查看基础标志。

 聚合标志以不同的大小绘制。 标志的大小取决于聚合中最重要的标志所具有的重要性级别。 下图按重要性从低到高显示聚合标志。

 ![显示四个重要性级别的聚合标志的插图。](../profiling/media/cvmarkeraggregate.png "CVMarkerAggregate")

## <a name="message-markers"></a>消息标记

消息标记代表日志输出。 消息是特定线程在特定时间发出的字符串。 可以将消息导出到文本文件，以便与其他工具一起使用。 可以将鼠标指针放在并发可视化工具中的某一消息上，以便查看消息字符串。 可以在[标记报告](../profiling/threads-view-reports.md#markers-report)中查看所有消息标记。  下图显示消息标记。

### <a name="message-aggregation-markers"></a>消息聚合标记
 有时，并发可视化工具中多个消息的发生时间过于接近，导致无法单独绘制。 发生这种情况时，将显示代表基础消息的消息聚合标记。 当将鼠标指针放在这些图标上时，工具提示将显示所代表的基础消息数量。 若要查看这些消息，请放大。  如果一直放大但仍显示聚合标记，则可在[标记报告](../profiling/threads-view-reports.md#markers-report)中查看基础消息。

## <a name="span-markers"></a>范围标记

范围标记表示应用程序一个有意义的阶段。 例如，可以用范围表示正在处理某特定工作项的时间间隔。 范围的长度表示相应的应用程序阶段的持续时间。 下图显示并发可视化工具中的一个范围：

 ![并发可视化工具中跨度标记的插图。](../profiling/media/cvmarkerspan.png "CVMarkerSpan")

### <a name="span-category"></a>范围类别
 范围标记可用 5 种不同的颜色显示，具体取决于其类别。 如果类别超过 5 个，则颜色将会重复。 类别可以是任意整数。 此图显示 5 种可能的颜色：

 ![不同类别中五个跨度的插图。](../profiling/media/cvmarkerspancategory.png "CVMarkerSpanCategory")

### <a name="span-aggregation-markers"></a>范围聚合标记
 有时，并发可视化工具中范围标记发生时间过于接近，导致无法单独绘制。 发生这种情况时，将会显示代表基础范围的灰色范围聚合标记。 当将鼠标指针放在这些图标上时，工具提示将显示所代表的基础范围数量。 若要查看范围，请放大。 如果一直放大但仍显示范围聚合标记，则可以在[标记报告](../profiling/threads-view-reports.md#markers-report)中查看基础范围标记。 此图显示范围聚合标记：

 ![并发可视化工具中聚合范围标记的插图。](../profiling/media/cvmarkerspanaggregate.png "CVMarkerSpanAggregate")

## <a name="see-also"></a>另请参阅
- [标志标记](../profiling/concurrency-visualizer-markers.md#flag-markers)
- [消息标记](../profiling/concurrency-visualizer-markers.md#message-markers)
- [范围标记](../profiling/concurrency-visualizer-markers.md#span-markers)
- [将 EventSource 事件作为标记可视化](../profiling/visualizing-eventsource-events-as-markers.md)