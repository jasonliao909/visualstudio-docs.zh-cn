---
title: 工作流设计器 - FlowSwitch&lt;T&gt; 活动设计器
description: 了解 FlowSwitch<T> 活动是如何成为一个条件节点，用于根据匹配条件为控制流提供分支。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Core.Presentation.FlowSwitchLink.UI
- System.Activities.Statements.FlowSwitch`1.UI
- System.Activities.Core.Presentation.FlowSwitchLink`1.UI
- System.Activities.Core.Presentation.FlowSwitchLinkIdentifier.UI
ms.assetid: 5b9c5afe-7499-4ee8-8c33-28aff14bde07
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: b5e3a400509668c7cab2310fcd4c67316f35b8ac
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665196"
---
# <a name="flowswitcht-activity-designer"></a>FlowSwitch\<T> 活动设计器

<xref:System.Activities.Statements.FlowSwitch%601> 活动是一个条件节点，它在需要两个以上备选分支时根据匹配条件分支控制流。 如果流分支仅需要两个路径，请改用 <xref:System.Activities.Statements.FlowDecision> 活动。

## <a name="the-flowswitcht-activity"></a>FlowSwitch\<T> 活动

<xref:System.Activities.Statements.FlowSwitch%601> 活动包含一个 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>，当对它进行计算时，将返回一个类型为 T 的值（由泛型参数指定）。 该活动还包含一组 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>，它指定从此计算的可能结果到一组 <xref:System.Activities.Statements.FlowNode> 对象的唯一映射。 执行的 <xref:System.Activities.Statements.FlowNode> 对象的类型 T 与计算的 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的值匹配。 可以选择在没有获得任何匹配时提供 <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> Case。

### <a name="using-the-flowswitcht-activity-designer"></a>使用 FlowSwitch\<T> 活动设计器

可以在“工具箱”的“流程图”类别中找到“FlowSwitch\<T>”活动设计器，通过单击工作流设计器左侧的“工具箱”选项卡来访问   。 或者，从“视图”菜单栏中选择“工具箱”或按 Ctrl+Alt+X    。

可以将“FlowSwitch\<T>”活动设计器从“工具箱”拖放到“流程图”活动设计器内的工作流设计器图面  。 使用显示的“选择类型”窗口指定通过计算 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的值而获得的类型（在代码中通过其泛型参数与 <xref:System.Activities.Statements.FlowSwitch%601> 关联）。 此过程将在 <xref:System.Activities.Statements.Flowchart> 活动中创建一个标记为“Switch”的 <xref:System.Activities.Statements.FlowSwitch%601> 活动。 在“属性”窗口的“表达式”框中，单击提示文本“输入 VB 表达式”所在位置即可键入 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 。

将鼠标悬停在“FlowSwitch\<T>”活动设计器上会导致其边缘周围出现用于链接 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 的正方形图柄。 将“FlowSwitch\>”活动设计器和其他活动设计器拖放到“流程图”上之后，它们所表示的 <xref:System.Activities.Activity> 对象即可链接在一起以指定执行顺序 。 若要创建与 <xref:System.Activities.Statements.FlowSwitch%601> 关联的一个 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>，请单击“FlowSwitch\>”周围的一个正方形事例图柄，并将其拖到（通过按住鼠标按钮）鼠标悬停在目标活动设计器上时该目标活动周围以类似方式显示的一个图柄。 松开鼠标按钮，此时将显示一个从“FlowSwitch\>”指向目标设计器的箭头，用于表示此事例。 此事例的默认值显示在该箭头上，并可在“属性”窗口的“事例”框中进行编辑 。

### <a name="the-flowswitcht-properties"></a>FlowSwitch\<T> 属性

下表列出 <xref:System.Activities.Statements.FlowSwitch%601> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>|True|指定表达式，通过计算该表达式来确定在执行路径中可切换到哪个 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>。|
|<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>|错误|指定通过从 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的可能计算结果到一组 <xref:System.Activities.Statements.FlowNode> 对象的唯一映射。|
|<xref:System.Activities.Statements.FlowSwitch%601.Default%2A>|True|指定当 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的计算值与 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 对象中包含的值之一不匹配时的映射。|

## <a name="see-also"></a>另请参阅

- [流程图](../workflow-designer/flowchart-activity-designers.md)
- [流程图](../workflow-designer/flowchart-activity-designer.md)
- [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)
