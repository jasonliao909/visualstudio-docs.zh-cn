---
title: 范围标记 | Microsoft Docs
description: 了解范围标记如何表示应用程序的有意义的阶段，并查看在并发可视化工具中显示范围的示例。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.markers.span
ms.assetid: 736b7765-9c71-44d7-85e5-79787d13d91c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 98fc9241a8f0bdcf4b92dfd4f1f745a1bfc8ea4f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736275"
---
# <a name="span-markers"></a>范围标记
范围标记表示应用程序一个有意义的阶段。 例如，可以用范围表示正在处理某特定工作项的时间间隔。 范围的长度表示相应的应用程序阶段的持续时间。 下图显示并发可视化工具中的一个范围：

 ![并发可视化工具中的范围标记](../profiling/media/cvmarkerspan.png "CVMarkerSpan") 并发可视化工具中的范围标记

## <a name="span-category"></a>范围类别
 范围标记可用 5 种不同的颜色显示，具体取决于其类别。 如果类别超过 5 个，则颜色将会重复。 类别可以是任意整数。 此图显示 5 种可能的颜色：

 ![不同类别中的 5 个范围](../profiling/media/cvmarkerspancategory.png "CVMarkerSpanCategory") 前 5 个范围类别的颜色

## <a name="span-aggregation-markers"></a>范围聚合标记
 有时，并发可视化工具中范围标记发生时间过于接近，导致无法单独绘制。 发生这种情况时，将会显示代表基础范围的灰色范围聚合标记。 当将鼠标指针放在这些图标上时，工具提示将显示所代表的基础范围数量。 若要查看范围，请放大。 如果一直放大但仍显示范围聚合标记，则可以在[标记报告](../profiling/markers-report.md)中查看基础范围标记。 此图显示范围聚合标记：

 ![并发可视化工具中的聚合范围](../profiling/media/cvmarkerspanaggregate.png "CVMarkerSpanAggregate") 范围聚合标记

## <a name="see-also"></a>另请参阅
- [并发可视化工具标记](../profiling/concurrency-visualizer-markers.md)
- [并发可视化工具 SDK](../profiling/concurrency-visualizer-sdk.md)