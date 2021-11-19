---
title: 工作流设计器 - Flowchart 活动设计器
description: 了解如何使用 Flowchart 活动来创建定义和管理复杂流控件的工作流。
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
ms.openlocfilehash: 948d4536f28440671fdba2a7a9931e0da66d7834
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666981"
---
# <a name="flowchart-activity-designer"></a>流程图活动设计器

<xref:System.Activities.Statements.Flowchart> 活动用于创建定义和管理复杂流控制的工作流。 可以使用代码或工作流设计器来创作 <xref:System.Activities.Statements.Flowchart>。 本主题介绍工作流设计器体验。 “工作流设计器”工作流活动设计器使开发人员能够以自然的方式创作工作流。

## <a name="the-flowchart-activity"></a>Flowchart 活动

<xref:System.Activities.Statements.Flowchart> 指定工作流启动时执行的唯一 <xref:System.Activities.Statements.Flowchart.StartNode%2A>，并使用链接的 <xref:System.Activities.Statements.Flowchart.Nodes%2A> 网络创建任意循环或将执行流在任意给定时间转移到工作流中的其他任何位置。

### <a name="using-the-flowchart-activity-designer"></a>使用 Flowchart 活动设计器

可以在“工具箱”的“流程图”类别中找到 Flowchart 活动设计器，通过单击工作流设计器的“工具箱”选项卡来访问   。 或者，从“视图”菜单栏中选择“工具箱”或按“Ctrl +Alt+X”    。

可以将 Flowchart 活动设计器从“工具箱”拖放到工作流设计器图面上的活动设计器通常放置的位置，可作为根活动，也可作为另一个控制流活动的子级 。 如果将 Flowchart 活动设计器放到一个空白的工作流设计器图面上，则会创建一个 <xref:System.Activities.Statements.Flowchart> 活动，默认情况下，该活动会以展开的视图呈现，其中启动执行的启动节点表示为一个绿球。 如果将 Flowchart 活动设计器放到另一个控制流活动中，则该活动会以最小化的视图显示，双击 Flowchart 活动设计器可展开该视图 。 “工具箱”中的任何活动（包括其他控制流活动）都可直接拖到 Flowchart 活动设计器中 。

将各种活动设计器拖到工作流设计器画布上之后，这些活动设计器表示的 <xref:System.Activities.Activity> 对象可链接在一起以指定执行顺序。 若要在源活动与目标活动之间创建链接，请将鼠标悬停在源活动的设计器上，此时将在该设计器的每一侧显示正方形处理框。 单击这些正方形处理框之一并按下鼠标按钮将其拖到当鼠标悬停在目标活动上时该活动周围以类似方式显示的处理框之一。 松开鼠标按钮，此时将在这两个活动之间创建一个链接，表示为从源设计器指向目标设计器的箭头。

### <a name="flowchart-activity-properties"></a>Flowchart 活动属性

下表列出 <xref:System.Activities.Statements.Flowchart> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定活动设计器在标头中的显示名称。 默认值为 Flowchart。 可以在“属性”窗口或直接在活动设计器标头中编辑该值。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.Flowchart.Variables%2A>|错误|作用范围在此 <xref:System.Activities.Statements.Flowchart> 内以在其子活动间共享状态的变量的集合。|
|<xref:System.Activities.Statements.Flowchart.StartNode%2A>|错误|在 <xref:System.Activities.Statements.FlowNode> 启动时执行的 <xref:System.Activities.Statements.Flowchart>。|
|<xref:System.Activities.Statements.Flowchart.Nodes%2A>|错误|包含 <xref:System.Activities.Statements.FlowNode> 中的 <xref:System.Activities.Statements.Flowchart> 对象的集合。|

## <a name="see-also"></a>另请参阅

- [流程图](../workflow-designer/flowchart-activity-designers.md)
- [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)
- [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)
