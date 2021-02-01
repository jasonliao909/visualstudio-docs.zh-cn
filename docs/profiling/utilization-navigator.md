---
title: 使用率导航器 | Microsoft Docs
description: 了解如何使用并发可视化工具中的使用率导航器来选择跟踪中的时间间隔。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.performance.utilizationnavigator
ms.assetid: 522a981a-37ef-4cdd-a04c-f1e7525a2aab
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9f209098200333e91f0e5baf9c7a2b73b4a3202f
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2021
ms.locfileid: "98723213"
---
# <a name="utilization-navigator"></a>使用率导航器
您可以使用并发可视化工具中的使用率导航器来选择跟踪中的时间间隔。 并发可视化工具显示目标进程在一段时间内的 CPU 内核使用率。 这样便于检查 CPU 使用率模式，还可以将使用率数据与其他视图中的数据进行比较。 使用率导航器显示在并发可视化工具的每个视图的顶部。 下图演示使用率导航器。

 ![显示选定期限的使用率导航器](../profiling/media/cvutilizationnavigator.png "CVUtilizationNavigator")使用率导航器和所选的期限

 在图中，选定的间隔由一个红色矩形来定义，称为 *thumb*。

 此处演示如何通过使用率导航器来操作所显示的时间范围：

- 可以通过左右拖动 Thumb 控件进行平移。 （键盘：将焦点移动到滚动块，然后按向左或向右键。）

- 通过拖动其中一个图柄，可以更改间隔的程度。 （键盘：将焦点移动到一个图柄，然后按向右或向左键。）

  如果使用另一种并发可视化工具缩放控件来更改间隔，则使用率导航器将会更新，以便反映所做的更改。