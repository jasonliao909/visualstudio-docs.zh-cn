---
title: 使用率视图 | Microsoft Docs
description: 了解“使用率”视图显示有关当前进程所使用的 CPU、GPU 和其他系统资源的信息。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.cpuutilization
- vs.cv.cpu.graph
- vs.cv.cpu.percentage
- vs.cv.cpu.zoom
- vs.cv.cpu.graph.gpu
- vs.cv.threads.timeline.gpuactivity
- vs.cv.threads.timeline.gpupaging
- vs.cv.threads.timeline.gpuexecution
- vs.cv.threads.timeline.gpuother
helpviewer_keywords:
- Concurrency Visualizer, CPU Utilization View
ms.assetid: b4f7ceab-3653-4069-bb74-c309aec62866
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: cdc8d2c567389cb1c97b54473a14fdfbba1cb947
ms.sourcegitcommit: caf5ca17efde4dc4de8b1bdfbe7770f6d705024d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2022
ms.locfileid: "145017655"
---
# <a name="utilization-view"></a>“使用率”视图

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]
“使用率”视图显示有关当前进程所使用的 CPU、GPU 和其他系统资源的信息（选择“分析” > “并发可视化工具”来启动并发可视化工具）。 它显示随着时间的推移，在系统上运行的分析的进程、空闲进程、系统进程和其他进程的平均核心使用率。 它不显示在某个给定时间哪个特定内核处于活动状态。 例如，如果两个内核在某一给定时间段内均以 50% 的使用率运行，则此视图将显示使用一个逻辑内核。 通过将分析时间分成较短的时间段生成此视图。 对于每个时间段，此图绘制出该间隔期间内在逻辑核心上执行的进程线程的平均数量。

 ![CPU 使用率视图](../profiling/media/vsts_ppacpuutil.png "VSTS_PPAcpuUtil")

 此图显示目标进程、空闲进程和系统进程所使用的时间（在 x 轴上）和平均的逻辑核心数量。 （空闲进程显示空闲内核。 系统进程是 Windows 中可代表其他进程执行工作的进程。）在系统上运行的剩余进程组成了所有剩余核心的使用率。

 逻辑核心数显示在 Y 轴上。 Windows 将硬件中的多线程并行处理支持视为逻辑核心（例如，超线程）。 因此，具有 4 核处理器且每核心支持两个硬件线程的系统显示为 8 逻辑核心的系统。 这同样也适用于“核心”视图。 有关详细信息，请参阅[“核心”视图](../profiling/cores-view.md)。

 GPU 活动关系图显示随着时间的推移，使用中的 DirectX 引擎数。  如果引擎正在处理 DMA 数据包，它则正在使用中。  该关系图不会显示特定的 DirectX 引擎（例如，3D 引擎、视频引擎等）。

## <a name="purpose"></a>用途

 我们建议在使用并发可视化工具时，将使用率视图作为性能调查的起点。 因为它概述了随着时间的推移，应用中的并发程，因此，可使用它快速识别需要进行性能调整或并行化的区域。

 如果对性能调整感兴趣，则可尝试识别不满足你期望的行为。 还可查找逻辑 CPU 核心使用率低的区域及原因。 此外，也可以查找 CPU 和 GPU 之间的使用模式。

 如果对并行化应用感兴趣，则可能会查找执行所占用大量 CPU 的区域或未使用 CPU 的区域。

 占用大量 CPU 的领域为绿色。 如果应用为串行，该图表则显示正在使用中的一个核心。

 未使用 CPU 的区域为灰色。 这些可能表示应用处于空闲状态或执行阻塞 I/O 的点，后者通过与其他占用大量 CPU 的工作重叠以提供进行并行的机会。

 找到感兴趣的行为后，可以通过选中该行为在该区域上进行放大。 缩放后，可以切换到“线程”视图或“核心”视图以了解更详细的分析。

 如果是通过 C++ AMP 或 DirectX 使用 GPU，则可能会对识别使用中的 GPU 引擎数或 GPU 在其中意外处于空闲状态的区域感兴趣。

## <a name="zoom"></a>Zoom

 若要在 CPU 使用率关系图或 GPU 活动关系图上放大，请选择某个节，或使用关系图顶部的缩放滑块工具。 当切换到其他视图时，缩放设置仍然存在。 若要再次缩小，请使用缩放滑块工具。 还可以使用 Ctrl+滚动条进行缩放。 

## <a name="cpu-utilization-graph"></a>CPU 使用率图

CPU 使用率图显示一段时间内应用中的使用程度。 X 轴表示跟踪的持续时间，Y 轴表示系统上的逻辑内核数。 此图形不显示在某个给定时间哪个特定内核处于活动状态。 例如，如果两个内核在某一给定时间段内均以 50% 的使用率运行，则此视图将显示使用一个逻辑内核。

### <a name="cpu-utilization-graph-colors"></a>CPU 使用率图颜色

- 绿色表示系统中当前进程的逻辑内核使用率。

- 浅灰色表示系统上其他进程的逻辑内核利用率。 如果 CPU 图中的浅灰色百分比过高，则表示其他进程已使系统负载过重，你的进程可能会被这些进程抢占资源。 若要减少其他进程使用的逻辑内核数，请减少系统上运行的逻辑内核数。

- 深灰色表示系统进程的逻辑内核消耗。 您无法直接控制这部分逻辑内核消耗，但由于这些消耗会影响您的进程可以使用的逻辑内核情况，因此了解这些消耗何时出现非常有用。

- 白色表示系统上未使用逻辑内核的可用性。 如果可以找到更多的并行机会，这些核心则可用于你的进程。

## <a name="average-cpu-utilization"></a>CPU 平均利用率

显示在进程持续时间内，已分析的进程对系统逻辑核心的平均利用率。 此图形不显示在某个给定时间哪个特定内核处于活动状态。 例如，如果两个内核在某一给定时间段内均以 50% 的使用率运行，则此视图将显示使用一个逻辑内核。

## <a name="zoom-control-utilization-view"></a>缩放控件（“使用率”视图）

缩放控件可帮助您放大 CPU 使用率图表，从而使您能够关注特定的感兴趣区域。 此控件可在视图的中心区域放大。 所以在放大之前将感兴趣的区域移到中心位置。

 在 CPU 使用率图表或 GPU 活动图中，可以拖动鼠标指针创建一个突出显示的区域。 释放鼠标按钮后，视图会放大选定的范围。

## <a name="gpu-activity-graph"></a>GPU 活动关系图

并发可视化工具中的 GPU 活动图显示系统上的 DirectX 活动级别，此活动级别通过一段时间内使用的 DirectX 引擎数来衡量。  此图不显示使用了哪些特定引擎。  如果引擎正在处理任意 GPU 工作，则将视为正在使用此引擎。

### <a name="gpu-activity-graph-colors"></a>GPU 活动关系图颜色

 绿色表示当前进程使用的 DirectX 引擎数。

 浅灰色表示系统上其他进程使用的 DirectX 引擎数。 若要减少其他进程使用的 DirectX 引擎数，请减少系统上运行的其他进程数。

 白色表示系统上未使用的 DirectX 引擎的可用性。 如果可以找到更多利用机会，这些引擎就可以用于您的进程。 一些引擎只能用于特定种类的任务。

## <a name="gpu-activity-paging"></a>GPU 活动(分页)

“线程”选项卡上的“GPU 活动(分页)”段表示 GPU 处理分页请求的时间。  段的长度代表 GPU 处理直接内存访问 (DMA) 数据包时的持续时间。 通常，分页数据包与 CPU 和 GPU 之间的内存转移有关。

 当选择某个 GPU 分页段时，“当前”选项卡上的报告将显示所处理的 DMA 数据包的相关信息。 这包括它在与 DirectX 引擎关联的硬件队列中等待的总时间、提交 DMA 数据包的进程，以及处理数据包所需的时间。

## <a name="gpu-activity-this-process"></a>GPU 活动(此进程)

在并发可视化工具中，“线程”视图中的“GPU 活动(此进程)”段表示 GPU 代表当前进程处理请求的时间。 这些请求以直接内存访问 (DMA) 数据包的形式发送到 GPU。 段的长度代表 GPU 代表当前进程处理 DMA 数据包的时间。

 当选择 GPU 活动段时，“当前”选项卡上的报告将显示所处理的 DMA 数据包的相关信息。 此信息包括数据包在与 DirectX 引擎关联的硬件队列中等待的总时间、提交数据包的进程，以及处理数据包所需的时间。 当前进程外的某个进程可能以物理方式将 DMA 数据包提交给了 GPU。 当另一个进程代表当前进程将工作提交给 GPU 时，并发可视化工具可以检测出来。

## <a name="gpu-activity-other-processes"></a>GPU 活动(其他进程)

并发可视化工具的“线程”视图中的“GPU 活动(其他进程)”段表示 GPU 代表系统上的其他进程处理请求的时间。 这些请求以直接内存访问 (DMA) 数据包的形式发送到 GPU。  段的长度代表 GPU 处理数据包的持续时间。

 当选择此类型段时，“当前”选项卡上的报告将显示所处理的数据包的相关信息。  此信息包括数据包在与 DirectX 引擎关联的硬件队列中等待的总时间、提交数据包的进程，以及处理数据包所需的时间。

## <a name="see-also"></a>另请参阅

- [并发可视化工具](../profiling/concurrency-visualizer.md)
- [“核心”视图](../profiling/cores-view.md)