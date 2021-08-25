---
title: “资源详细信息”视图 - 争用数据 | Microsoft Docs
description: 了解“资源详细信息”视图如何显示针对所选资源的争用所导致的阻塞事件的时间线关系图。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.resourcedetails
helpviewer_keywords:
- Resource Details view
ms.assetid: a4ecfe1c-abbc-4fb3-9ab2-34de50486901
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 3e07b658d28cfbc91e8c9ea3d3613f201be1146e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122054517"
---
# <a name="resource-details-view---contention-data"></a>“资源详细信息”视图 - 争用数据
“资源详细信息”视图显示针对所选资源的争用所导致的阻塞事件的时间线关系图。 如果由于另一个线程已锁定对资源的访问，因此线程被迫挂起执行，则会发生阻塞事件。

 此视图将每个线程的执行时间线表示为水平条，而将每个阻塞事件表示为线程时间线上的垂直条。 如有必要，可以放大时间线的每个部分以查看单个事件。 若要查看导致事件的函数的执行路径（调用堆栈），请单击事件条。 函数会出现在“调用堆栈”窗口中。 当函数的源代码可用时，可以单击函数名，以便在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的界面中编辑源文件。

## <a name="procedures"></a>过程

#### <a name="to-magnify-a-timeline-segment"></a>放大时间线片段

- 将鼠标指针拖动到时间线的某个区域上。

     释放鼠标按钮后，视图会放大到所选时间片段。 可以重复该过程以进一步放大片段。 时间滚动条上的滚动框表示出现在视图中的时间片段的相对大小。

#### <a name="to-zoom-out-on-a-timeline"></a>缩小时间线

- 执行以下步骤之一：

  - 单击“缩小”以返回到以前的缩放级别。

  - 单击“缩放重置”以在视图中显示所有时间线。

#### <a name="to-view-the-call-stack-of-an-event"></a>查看事件的调用堆栈

- 在时间线关系图中，单击事件条。

#### <a name="to-view-or-edit-the-source-code-of-a-function-in-the-call-stack"></a>查看或编辑调用堆栈中的函数的源代码

- 在“调用堆栈”窗口中，单击函数名。

  函数源代码必须是当前项目的一部分。

#### <a name="to-view-the-call-tree-of-contention-events-for-the-resource"></a>查看资源的争用事件的调用树

- 在时间线关系图中，单击“总计”。

     资源的“争用”视图会出现。 有关详细信息，请参阅[“资源争用”视图](../profiling/resource-contentions-view-contention-data.md)。

#### <a name="to-view-all-the-contention-events-of-a-thread"></a>查看线程的所有争用事件

- 在时间线关系图中，单击线程的名称或 ID。

     所选线程的“线程详细信息”视图会出现。 有关详细信息，请参阅[“线程详细信息”视图](../profiling/thread-details-view-contention-data.md)。
