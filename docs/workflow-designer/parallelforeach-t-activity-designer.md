---
title: ParallelForEach&lt;T&gt; 活动设计器
description: 在工作流设计器中，了解 ParallelForEach <T> 活动如何枚举集合元素并对集合中的每个元素并行执行嵌入语句。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ParallelForEach`1.UI
ms.assetid: e93a4843-aef2-4d3e-9a0a-a2d3d1411aa7
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 07158b14beca37272c19f4a5b896d7c70223a667
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666108"
---
# <a name="parallelforeach-activity-designer"></a>ParallelForEach 活动设计器

<xref:System.Activities.Statements.ParallelForEach%601> 活动枚举集合元素并对集合中的每个元素并行执行嵌入语句，这将在同一线程上异步执行。 如果此活动的子活动预期会进入空闲状态，请使用此流控制活动，而不是 <xref:System.Activities.Statements.Sequence> 活动。

<xref:System.Activities.Statements.ParallelForEach%601> 活动有一个 <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> 属性，该属性包含用户指定的 Visual Basic 表达式。 <xref:System.Activities.Statements.ParallelForEach%601> 活动在完成每个分支后计算此属性。 如果计算结果为 true，则 <xref:System.Activities.Statements.ParallelForEach%601> 活动完成，无需执行其他分支。 如果 <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> 计算结果不为 true，则 <xref:System.Activities.Statements.ParallelForEach%601> 活动在完成其所有子活动后完成。

## <a name="the-parallelforeacht-activity"></a>The ParallelForEach<T\> 活动

<xref:System.Activities.Statements.ParallelForEach%601> 枚举其值并为枚举的每个值安排 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A>。 仅安排 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 的执行顺序。 Body 的执行方式取决于 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 是否进入空闲状态。

如果 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 未进入空闲状态，则会按相反顺序执行，因为安排的活动作为堆栈来处理，最后安排的活动最先执行。 例如，如果在 <xref:System.Activities.Statements.ParallelForEach%601> 中有一个集合 {1,2,3,4}，并使用 WriteLine 作为正文来写入值。将在控制台中打印 4、3、2、1。 这是因为 WriteLine 未进入空闲状态，因此在安排 4 个 WriteLine 活动之后，会使用堆栈行为（先进后出）执行这些活动 。

但是如果 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 中有会进入空闲状态的活动，如 <xref:System.ServiceModel.Activities.Receive> 活动或 <xref:System.Activities.Statements.Delay> 活动， 那么就不需要等待它们完成。 <xref:System.Activities.Statements.ParallelForEach%601> 转至下一个预定的主体活动，并尝试执行它。 如果该活动也进入空闲状态，则 <xref:System.Activities.Statements.ParallelForEach%601> 将再移到下一个 Body 活动。

### <a name="using-the-parallelforeacht-activity-designer"></a>使用 ParallelForEach\<T> 活动设计器

访问“工具箱”的“控制流”类别中的 ParallelForEach\<T> 活动设计器  。

可以将 ParallelForEach\<T> 活动设计器从“工具箱”拖放到工作流设计器图面上通常放置活动设计器的任何位置，例如，在 Sequence 活动设计器内  。 将该活动设计器拖放到工作流设计器中之后，它会创建一个 <xref:System.Activities.Statements.ParallelForEach%601> 活动，该活动默认情况下包含 ParallelForEach<Int32\> 的 <xref:System.Activities.Activity.DisplayName%2A>。

### <a name="parallelforeacht-properties-in-the-workflow-designer"></a>工作流设计器中的 ParallelForEach<T\> 属性

下表列出最有用的 <xref:System.Activities.Statements.ParallelForEach%601> 活动属性并说明如何在设计器中使用它们。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定活动设计器在标头中的友好显示名称。 默认值为 ParallelForEach\<Int32>。 可以在“属性”网格中编辑该值，或直接在活动设计器标头中编辑该值。|
|<xref:System.Activities.Statements.ParallelForEach%601.Body%2A>|错误|要为集合中的每一项执行的活动。 若要添加 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> 活动，请将活动从工具箱拖放到 ParallelForEach\<T> 活动设计器上带提示文本“将活动拖放到此处”的“主体”框中 。|
|**TypeArgument**|True|<xref:System.Activities.Statements.ParallelForEach%601.Values%2A> 集合中的项的类型，由泛型参数 T 指定。默认情况下，“TypeArgument”设置为“Int32” 。 若要更改 ParallelForEach<T\> 活动设计器中的类型 T，请在属性网格中更改 TypeArgument 组合框的值 。|
|<xref:System.Activities.Statements.ParallelForEach%601.Values%2A>|True|要循环访问的项的集合。 若要设置 <xref:System.Activities.Statements.ParallelForEach%601.Values%2A>，请在 ForEach<T\> 活动设计器上带提示文本“输入 VB 表达式”的“值”框或在“属性”窗口的“值”框中键入 Visual Basic 表达式   。|
|<xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A>||在每个迭代完成后计算。 如果其计算结果为 true，则取消已安排的挂起的迭代。 如果未设置此属性，则所有安排的语句都将执行，直至完成为止。|

默认情况下，循环迭代器是命名项。 可在 ParallelForEach\<T> 活动设计器的 ForEach 框中更改迭代器变量的名称 。 循环迭代器可在 <xref:System.Activities.Statements.ParallelForEach%601> 活动的子级中的表达式中使用。

## <a name="see-also"></a>另请参阅

- [序列](../workflow-designer/sequence-activity-designer.md)
- [Parallel](../workflow-designer/parallel-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)