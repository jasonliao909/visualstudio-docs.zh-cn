---
title: 工作流设计器 - 并行活动设计器
description: 了解 Parallel 活动，以及如何使用并行活动设计器并发执行子活动的集合。
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

<xref:System.Activities.Statements.Parallel>活动具有一 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> 个 属性，该属性包含用户指定的Visual Basic表达式。 <xref:System.Activities.Statements.Parallel> 活动在完成每个分支后计算此属性。 如果计算结果为 **True，** 则 <xref:System.Activities.Statements.Parallel> 活动完成，而不执行其他分支。 如果 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> 计算结果不 **为 True，** 则活动在其所有子活动完成 <xref:System.Activities.Statements.Parallel> 时完成。

### <a name="using-the-parallel-activity-designer"></a>使用 Parallel 活动设计器

访问 **"工具箱**"的"控件 **Flow控件"** 类别中的 **"并行"活动设计器**。

并行 **活动** 设计器可以从"工具箱"拖动，并拖放到工作流设计器图面上，而不管活动设计器通常位于何处（例如，在序列活动 **设计器内）。** 在将活动工作流设计器，它会创建一个 活动，该活动 <xref:System.Activities.Statements.Parallel> 默认包含 <xref:System.Activities.Activity.DisplayName%2A> Parallel 的

若要将活动添加到并行活动的集合，请从"工具箱"拖动一些其他活动设计器，并将其拖放到"并行"活动 <xref:System.Activities.Statements.Parallel.Branches%2A> **设计器** 内的三角形上。 三角形位于分支中包含的活动的侧面。 可通过重复此过程过来添加其他活动。 可以通过在 Parallel 活动设计器中拖放活动来重新 **排列** 活动。

### <a name="parallel-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 Parallel 活动属性

下表列出 Parallel 活动属性并说明如何在设计器中使用这些属性。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定活动设计器在标头中的友好显示名称。 默认值为 **Parallel**。 可以选择在"属性"网格中编辑 **该值，也可以** 直接在活动设计器标头上编辑该值。|
|<xref:System.Activities.Statements.Parallel.Branches%2A>|True|包含要执行的子活动的集合。|
|<xref:System.Activities.Statements.Parallel.CompletionCondition%2A>|错误|在分支完成后计算。 如果计算结果为 **True，** 则取消计划的挂起分支。 如果未设置此属性或计算结果为 **False**，则当活动的所有子活动都已完成时，活动将完成。 默认值为 **null**。|

## <a name="see-also"></a>另请参阅

- [序列](../workflow-designer/sequence-activity-designer.md)
- [ParallelForEach\<T>](../workflow-designer/parallelforeach-t-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)
