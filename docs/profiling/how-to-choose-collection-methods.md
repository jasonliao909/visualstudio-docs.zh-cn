---
title: 选择收集方法 | Microsoft Docs
description: Visual Studio 分析工具支持三种收集性能数据的方法。 了解如何选择应用程序所需的方法。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- performance tools, choosing collection method
- profiling tools, choosing collection method
- performance collection methods
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: d2a79f24d2d9b3c8a9ea2bd0844f3d2ff3279a0d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126642391"
---
# <a name="how-to-choose-collection-methods"></a>如何：选择收集方法

Visual Studio 分析工具支持三种收集性能数据的方法：采样、检测和并发。 还可以使用采样或检测方法收集 .NET 内存分配和生存期数据。

可以使用性能会话“方法”属性指定最适合应用程序的收集方法。 可从“性能向导”、“性能资源管理器”或性能会话的“属性”页中选择收集方法。 有关使用命令行工具的详细信息，请参阅[命令行分析](../profiling/using-the-profiling-tools-from-the-command-line.md)。

## <a name="performance-wizard"></a>性能向导

### <a name="to-select-a-collection-method-using-the-performance-wizard"></a>使用“性能向导”选择收集方法

- 在向导的第一页上，选择下列选项之一：

| 选项 | 描述 |
|----------------------------| - |
| **CPU 采样** | 收集对初始分析和分析 CPU 使用率问题非常有用的应用程序统计信息。 |
| **检测** | 收集对重点分析和分析输入/输出性能问题非常有用的详细的计时数据。 |
| **.NET 内存分配** | 使用采样分析方法收集 .NET Framework 内存分配数据。 |
| **并发** | 收集数字资源争用数据。 |

## <a name="performance-explorer"></a>性能资源管理器

### <a name="to-select-a-collection-method-using-performance-explorer"></a>使用“性能资源管理器”选择收集方法

1. 在“性能资源管理器”工具栏上，单击“方法”下拉列表旁的箭头。

2. 单击想选择的收集方法。

## <a name="performance-session-property-pages"></a>性能会话属性页

### <a name="to-select-the-sampling-or-instrumentation-method-using-performance-session-properties"></a>使用性能会话属性选择采样或检测方法

1. 在“性能资源管理器”中，选择性能会话。

     性能会话文件的扩展名为 .psess。

2. 右键单击性能会话，然后单击“属性”。

3. 在“属性页”中，单击“常规”。

4. 单击想选择的收集方法。

    - 有关收集采样数据时其他可用选项的信息，请参阅[使用采样收集性能统计信息](../profiling/collecting-performance-statistics-by-using-sampling.md)

    - 有关收集采样数据时其他可用选项的信息，请参阅[使用检测收集详细计时数据](../profiling/collecting-detailed-timing-data-by-using-instrumentation.md)。

### <a name="to-select-net-memory-data-collection-by-using-performance-session-properties"></a>使用性能会话属性选择 .NET 内存数据收集

1. 在“性能资源管理器”中，选择性能会话。

     性能会话文件的扩展名为 .psess。

2. 右键单击性能会话，然后单击“属性”。

3. 在“属性页”中，单击“常规”。

4. 单击“采样”或“检测”。

5. 单击“收集 .NET 对象分配信息”收集 .NET Framework 对象分配的大小和数量。

6. （可选）单击“同时收集 .NET 对象的生存期信息”收集有关对象内存回收在其中的垃圾回收生成的数据。

     有关收集 .NET 内存数据时的其他可用选项的信息，请参阅[收集 .NET 内存分配和生存期数据](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)。

### <a name="to-select-concurrency-data-collection-by-using-performance-session-properties"></a>使用性能会话属性选择并发数据收集

1. 在“性能资源管理器” 中，右键单击性能会话，然后单击“属性” 。

2. 在“属性页”中，单击“常规”。

3. 单击“并发”。

## <a name="see-also"></a>请参阅

[配置性能会话](../profiling/configuring-performance-sessions.md)
[了解采样数据值](../profiling/understanding-sampling-data-values.md)
[性能会话属性](../profiling/performance-session-properties.md)
