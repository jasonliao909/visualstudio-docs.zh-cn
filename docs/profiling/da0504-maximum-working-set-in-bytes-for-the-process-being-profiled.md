---
title: DA0504 - 所分析的进程的最大工作集（以字节为单位）| Microsoft Docs
description: 此消息用于报告此进程当前使用的最大物理内存量（以字节为单位）。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.DA0504
- vs.performance.504
- vs.performance.rules.DA0504
ms.assetid: 36e71603-ece7-4000-85fc-9da4eed61bf2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 5e72f83038724d2b3e05e2bee33dc6d8fcaedb1c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122142112"
---
# <a name="da0504-maximum-working-set-in-bytes-for-the-process-being-profiled"></a>DA0504：所分析进程的最大工作集（字节）

|项|“值”|
|-|-|
|规则 ID|DA0504|
|类别|资源管理|
|分析方法|全部|
|消息|收集此信息仅用于参考。 进程工作集计数器测量由正在分析的进程使用的物理内存的使用情况。 报告的值是在所有测量时间间隔内观察到的最大值。|
|规则类型|信息|

 使用采样法、.NET 内存或资源争用方法进行分析时，必须收集至少 10 个样本才能触发此规则。

## <a name="rule-description"></a>规则说明
 此消息用于报告此进程当前使用的最大物理内存量（以字节为单位）。 进程工作集表示当前位于物理内存中的进程地址空间中的页面。 此规则报告分析处于活动状态时进程工作集的最大值。

 报告的值包括进程已引用的共享内存段中的驻留页面。 进程引用的共享 DLL 包含在计算的共享内存段中。 受共享内存段的影响，进程工作集的值可能高于进程已经分配的虚拟内存量。

 进程工作集的大小反映进程当前使用的虚拟内存量。 它还受可用于运行应用程序的物理内存量（或 RAM）和其他运行的进程对该物理内存的争用量的影响。 有关进程工作集的详细信息，请参阅 MSDN 上 Windows 内存管理文档中的 [Working Set](/windows/win32/memory/working-set)（工作集）。

## <a name="how-to-use-rule-data"></a>如何使用规则数据
 该规则从 Windows 性能监视设备收集此测量数据，并进行报告用于信息用途。 若要了解不同测试方案中应用程序的性能，可使用此规则比较不同版本程序的性能。

 双击“错误列表”窗口中的消息，导航到分析数据的[标记视图](../profiling/marks-view.md)。 查找 **Process\Working Set** 和 **Memory\Pages/sec** 计数器列。 然后，查找 **Process\Working Set** 的最大值，并将其与 **Memory\Pages/sec** 值比较。 通常情况下，工作集与时间间隔相关联，此时分页 IO 活动会减少（尤其当计算机是内存约束的时候）。
