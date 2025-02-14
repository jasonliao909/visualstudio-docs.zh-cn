---
title: “进程属性”对话框 ->“内存”选项卡 | Microsoft Docs
description: 使用“进程属性”的“内存”选项卡来查看进程如何使用内存。 其中包含有关使用的空间、共享的空间和使用的虚拟空间的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Process properties for Windows NT
ms.assetid: a70785f2-5997-40ec-a90f-80a52449768b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 65171b796f440bc612bb7e0802bacd2373b23eb6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126644279"
---
# <a name="memory-tab-process-properties-dialog-box"></a>“进程属性”对话框 ->“内存”选项卡
使用“内存”选项卡可显示进程如何使用内存。 若要显示[“进程属性”对话框](../debugger/process-properties-dialog-box.md)，请将焦点移动到[进程视图](../debugger/processes-view.md)窗口。 在树中选择任意进程节点，然后从“视图”菜单选择“属性” 。

 “内存”选项卡上有以下可用设置：

|条目|描述|
|-----------|-----------------|
|**虚拟字节数**|进程所使用虚拟地址空间的当前大小（字节）。 使用虚拟地址空间并不一定意味着要相应使用磁盘或主内存页。 不过，虚拟空间是有限的，使用过多虚拟空间可能会限制进程加载库的能力。|
|**峰值虚拟字节数**|进程在任一时间使用的虚拟地址空间的最大字节数。|
|**工作集**|进程中的线程最近使用过的内存页的集合。 如果计算机中的可用内存高于阈值，则即使内存页未被使用，它们也会保留在进程的工作集中。 如果可用内存降到阈值以下，则会从工作集中削减页。 如果需要它们，在其离开主内存之前，系统会将它们软恢复到工作集中。|
|**峰值工作集**|在任意时间点此进程的工作集中的最大页数。|
|**分页缓冲池字节数**|进程已分配的当前分页缓冲池量。 分页缓冲池是一个系统内存区域，在该区域中，操作系统组件在其完成其指定任务时会获取空间。 当系统在持续的一段时间内未访问分页缓冲池页时，可以将其调出为页文件。|
|**非分页缓冲池字节数**|由进程分配的非分页缓冲池中的当前字节数。 非分页缓冲池是一个系统内存区域，在该区域中，操作系统组件在其完成其指定任务时会获取空间。 无法将非分页缓冲池页调出为页文件；只要对它们进行了分配，它们就会保留在主内存中。|
|**专用字节数**|此进程已分配但不能与其他进程共享的当前字节数。|
|**可用字节数**|此进程未使用的虚拟地址空间总数。|
|**保留字节数**|此进程保留供将来使用的虚拟内存总量。|
|**可用图像字节数**|此进程中图像未使用或保留的虚拟地址空间量。|
|**保留图像字节数**|此进程中运行的图像所保留的所有虚拟内存的总和。|