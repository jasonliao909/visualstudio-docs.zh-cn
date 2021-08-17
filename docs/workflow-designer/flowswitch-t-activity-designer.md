---
title: 工作流设计器 - FlowSwitch &lt; T &gt; 活动设计器
description: 了解 FlowSwitch 活动如何是基于匹配条件为控制流 <T> 提供分支的条件节点。
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
ms.openlocfilehash: 6aa40da33fba5ae7f95e41fff6a2d905fc0585f64cab88d2d2cb0d4340cf8ccc
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121383776"
---
# <a name="flowswitcht-activity-designer"></a>FlowSwitch\<T> 活动设计器

<xref:System.Activities.Statements.FlowSwitch%601> 活动是一个条件节点，它在需要两个以上备选分支时根据匹配条件分支控制流。 如果流分支仅需要两个路径，请改用 <xref:System.Activities.Statements.FlowDecision> 活动。

## <a name="the-flowswitcht-activity"></a>FlowSwitch \<T> 活动

<xref:System.Activities.Statements.FlowSwitch%601>活动包含一 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 个 ，它返回由泛型 (在计算时指定的) T 值。 该活动还包含一组 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>，它指定从此计算的可能结果到一组 <xref:System.Activities.Statements.FlowNode> 对象的唯一映射。 执行的 <xref:System.Activities.Statements.FlowNode> 是类型 *为 T* 的对象与所计算 的值匹配的 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 对象。 可以选择在没有获得任何匹配时提供 <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> Case。

### <a name="using-the-flowswitcht-activity-designer"></a>使用 FlowSwitch \<T> 活动设计器

可以在"工具箱"的"流程图"类别中找到 **FlowSwitch \<T>** 活动设计器，单击"工具箱"左侧的"工具箱"选项卡即可工作流设计器。 或者，从"视图 **"菜单中** 选择"**工具箱"，** 或按 **Ctrl** + **Alt** + **X**。

可以从 **"工具箱"拖动 \<T> FlowSwitch** 活动设计器，工作流设计器 **流图活动设计器** 中的流图面。 使用显示的 **"** 选择类型"窗口， (通过从计算 获取的泛型参数) 在代码中 <xref:System.Activities.Statements.FlowSwitch%601> 关联的类型 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 。 此过程在活动中 <xref:System.Activities.Statements.FlowSwitch%601> 创建标记为 **"Switch"** <xref:System.Activities.Statements.Flowchart> 的活动。 可以通过 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 单击提示文本显示"输入表达式"的位置，在"属性"窗口的"表达式"VB键入 。

将鼠标悬 **停在 FlowSwitch \<T>** 活动设计器上，使用于向上链接的正方形图柄 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 出现在其边缘周围。 将 **FlowSwitch<T \>** 活动设计器和其他活动设计器拖动到流程图上后，它们表示的对象就可以链接在一起以指定 <xref:System.Activities.Activity> 执行顺序。 若要创建与 关联的 之一，请单击 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> <xref:System.Activities.Statements.FlowSwitch%601> **FlowSwitch<\>** (T 外围上的一个正方形图柄，然后按住鼠标按钮) 将其拖动到鼠标悬停在其设计器上时以类似方式出现在目标活动的其中一个句柄上。 将鼠标按钮和从 **FlowSwitch \>**<T 到目标设计器的箭头显示，表示这种情况。 此用例的默认值显示在箭头上，可以在"属性"窗口的"**案例"框中****编辑**。

### <a name="the-flowswitcht-properties"></a>FlowSwitch \<T> 属性

下表列出 <xref:System.Activities.Statements.FlowSwitch%601> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>|正确|指定表达式，通过计算该表达式来确定在执行路径中可切换到哪个 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>。|
|<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>|错误|指定通过从 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的可能计算结果到一组 <xref:System.Activities.Statements.FlowNode> 对象的唯一映射。|
|<xref:System.Activities.Statements.FlowSwitch%601.Default%2A>|正确|指定当 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 的计算值与 <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 对象中包含的值之一不匹配时的映射。|

## <a name="see-also"></a>请参阅

- [流程图](../workflow-designer/flowchart-activity-designers.md)
- [流程图](../workflow-designer/flowchart-activity-designer.md)
- [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)
