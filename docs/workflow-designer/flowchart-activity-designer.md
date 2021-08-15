---
title: 工作流设计器 - 流程图活动设计器
description: 了解如何使用流程图活动创建定义和管理复杂流控件的工作流。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Flowchart.UI
- System.Activities.Statements.FlowStep.UI
- System.Activities.Core.Presentation.FlowStart.UI
ms.assetid: d5af2276-5215-4138-880a-cf2b90bbf3a0
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: e6b00356debe67e87410a1be9112af59c305906096d96a34417802b1fd917dcf
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121408053"
---
# <a name="flowchart-activity-designer"></a>流程图活动设计器

<xref:System.Activities.Statements.Flowchart> 活动用于创建定义和管理复杂流控制的工作流。 <xref:System.Activities.Statements.Flowchart>可以在代码中创作 ，也可使用 工作流设计器。 本主题介绍工作流设计器体验。 开发人员工作流设计器工作流活动设计器以自然方式创作工作流。

## <a name="the-flowchart-activity"></a>Flowchart 活动

<xref:System.Activities.Statements.Flowchart> 指定工作流启动时执行的唯一 <xref:System.Activities.Statements.Flowchart.StartNode%2A>，并使用链接的 <xref:System.Activities.Statements.Flowchart.Nodes%2A> 网络创建任意循环或将执行流在任意给定时间转移到工作流中的其他任何位置。

### <a name="using-the-flowchart-activity-designer"></a>使用 Flowchart 活动设计器

**可以在"工具箱**"的"流程图"类别中找到流程图活动设计器，单击"工具箱"选项卡即可工作流设计器。  或者，从"视图 **"菜单中** 选择"**工具箱"，** 或按 **Ctrl** + **Alt** + **X**。

可以将 **流程图** 活动设计器从"工具箱"拖动到工作流设计器 图面上，无论活动设计器通常作为根活动还是作为另一个控制流活动的子级放置。 如果将 **流程图** 活动设计器放到空白的 工作流设计器 图面上，它将创建一个 活动，默认情况下，该活动在展开的视图中显示，其中启动执行的启动节点表示 <xref:System.Activities.Statements.Flowchart> 为绿色球。 如果 **流程图活动** 设计器被放入另一个控制流活动，它将自身呈现在最小化视图中，该视图可通过双击流程图活动 **设计器进行扩展** 。 工具箱中的任何 **活动** 都可以直接拖动到 **流程** 图活动设计器上，包括其他控制流活动。

将各种活动设计器拖动工作流设计器画布上后，可以将其表示的对象链接在一起以 <xref:System.Activities.Activity> 指定执行顺序。 若要在源活动与目标活动之间创建链接，请将鼠标悬停在源活动的设计器上，此时将在该设计器的每一侧显示正方形处理框。 单击这些正方形处理框之一并按下鼠标按钮将其拖到当鼠标悬停在目标活动上时该活动周围以类似方式显示的处理框之一。 松开鼠标按钮，此时将在这两个活动之间创建一个链接，表示为从源设计器指向目标设计器的箭头。

### <a name="flowchart-activity-properties"></a>Flowchart 活动属性

下表列出 <xref:System.Activities.Statements.Flowchart> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定活动设计器在标头中的显示名称。 默认值为 Flowchart。 可以在"属性"窗口中编辑 **该值，也可以** 直接在活动设计器标头上编辑该值。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.Flowchart.Variables%2A>|错误|作用范围在此 <xref:System.Activities.Statements.Flowchart> 内以在其子活动间共享状态的变量的集合。|
|<xref:System.Activities.Statements.Flowchart.StartNode%2A>|错误|在 <xref:System.Activities.Statements.FlowNode> 启动时执行的 <xref:System.Activities.Statements.Flowchart>。|
|<xref:System.Activities.Statements.Flowchart.Nodes%2A>|错误|包含 <xref:System.Activities.Statements.FlowNode> 中的 <xref:System.Activities.Statements.Flowchart> 对象的集合。|

## <a name="see-also"></a>另请参阅

- [流程图](../workflow-designer/flowchart-activity-designers.md)
- [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)
- [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)
