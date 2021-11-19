---
title: 工作流设计器 - Parallel 活动设计器
description: 了解 Parallel 活动，以及如何使用 Parallel 活动设计器并发执行子活动集合。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Parallel.UI
ms.assetid: 0306dc3b-075a-4091-ac3a-96486fbabed5
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: d4b1c5315933e2e29e29774b94804846d5317723
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666977"
---
# <a name="parallel-activity-designer"></a>Parallel 活动设计器

<xref:System.Activities.Statements.Parallel> 活动并发执行一组子活动。

## <a name="the-parallel-activity"></a>Parallel 活动

<xref:System.Activities.Statements.Parallel> 活动将其子活动存储在 <xref:System.Activities.Statements.Parallel.Branches%2A> 集合中。 如果某些子活动可能进入空闲状态，则使用 <xref:System.Activities.Statements.Parallel> 活动，而不使用 <xref:System.Activities.Statements.Sequence> 活动。

<xref:System.Activities.Statements.Parallel> 活动有一个 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> 属性，该属性包含用户指定的 Visual Basic 表达式。 <xref:System.Activities.Statements.Parallel> 活动在完成每个分支后计算此属性。 如果计算结果为 True，则 <xref:System.Activities.Statements.Parallel> 活动完成，无需执行其他分支。 如果 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> 计算结果不为 True，则 <xref:System.Activities.Statements.Parallel> 活动在完成其所有子活动后完成。

### <a name="using-the-parallel-activity-designer"></a>使用 Parallel 活动设计器

访问“工具箱”的“控制流”类别中的 Parallel 活动设计器。

可以将 Parallel 活动设计器从“工具箱”拖放到工作流设计器图面上通常放置活动设计器的任何位置，例如，在 Sequence 活动设计器内。 将该活动设计器拖放到工作流设计器中之后，它会创建一个 <xref:System.Activities.Statements.Parallel> 活动，该活动默认情况下包含 Parallel 的 <xref:System.Activities.Activity.DisplayName%2A>

若要向 Parallel 活动的 <xref:System.Activities.Statements.Parallel.Branches%2A> 集合添加活动，请将其他活动设计器从“工具箱”拖放到“Parallel”活动设计器内的三角形上。 三角形位于分支中包含的活动的侧面。 可通过重复此过程过来添加其他活动。 通过在 Parallel 活动设计器内拖放活动，可对其重新排序。

### <a name="parallel-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 Parallel 活动属性

下表列出 Parallel 活动属性并说明如何在设计器中使用这些属性。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定活动设计器在标头中的友好显示名称。 默认值为“Parallel”。 可以在“属性”网格中编辑该值，或直接在活动设计器标头中编辑该值。|
|<xref:System.Activities.Statements.Parallel.Branches%2A>|True|包含要执行的子活动的集合。|
|<xref:System.Activities.Statements.Parallel.CompletionCondition%2A>|错误|在分支完成后计算。 如果其计算结果为 True，则取消已安排的挂起分支。 如果未设置此属性或其计算结果为 False，则活动在完成其所有子活动后完成。 默认值为 **null**。|

## <a name="see-also"></a>另请参阅

- [序列](../workflow-designer/sequence-activity-designer.md)
- [ParallelForEach\<T>](../workflow-designer/parallelforeach-t-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)
