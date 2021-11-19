---
title: 工作流设计器 - State 活动设计器
description: 了解 StateMachine 活动，以及如何使用 State 活动设计器向工作流添加状态。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.State.UI
ms.assetid: 9455ab37-93a0-4c46-9eb8-b6611ca23167
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 2a0d23bedea24a68285e90faf8ee39fd46de90fc
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666104"
---
# <a name="state-activity-designer"></a>状态活动设计器

<xref:System.Activities.Statements.State> 表示状态机可具有的状态。

## <a name="using-the-state-activity-designer"></a>使用 State 活动设计器

要将 <xref:System.Activities.Statements.State> 添加到工作流，请将“State”活动设计器从“工具箱”的“状态机”部分拖放到工作流设计器图面上的 <xref:System.Activities.Statements.StateMachine> 活动  。 <xref:System.Activities.Statements.State> 活动可以放置到 <xref:System.Activities.Statements.StateMachine>，以后可添加转换；或在删除 <xref:System.Activities.Statements.State> 活动时可创建转换。 要在一个步骤中添加 <xref:System.Activities.Statements.State> 活动并创建转换，请拖动“工具箱”的“状态机”部分中的“State”活动并将它悬停在工作流设计器中的另一状态上  。 在另一个 <xref:System.Activities.Statements.State> 上拖动 <xref:System.Activities.Statements.State> 时，在另一个 <xref:System.Activities.Statements.State> 周围将出现四个三角形。 如果将 <xref:System.Activities.Statements.State> 放置到其中一个三角形，则将其添加到状态机，而且创建从源 <xref:System.Activities.Statements.State> 到放置目标 <xref:System.Activities.Statements.State> 的转换。 有关详细信息，请参阅[转换](../workflow-designer/transition-activity-designer.md)。

### <a name="state-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 State 活动属性

下表列出可使用工作流设计器设置的 <xref:System.Activities.Statements.State> 属性并说明如何在设计器中使用它们。 其中一些属性可以在属性网格中进行编辑，另一些属性可以在设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Statements.State.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.State> 活动设计器在标头中的友好名称。 默认值为“State”。 可以在属性网格或直接在活动设计器的标头中编辑该值。 <xref:System.Activities.Statements.State.DisplayName%2A> 用于痕迹导航，后者显示在工作流设计器顶部。<br /><br /> 虽然 <xref:System.Activities.Statements.State.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.State.Entry%2A>|错误|指定在转换到此状态时发生的操作。 展开 <xref:System.Activities.Statements.State> 活动时，可以通过从“工具箱”拖动某个活动并将其放置到状态的“进入”部分来设置此值 。|
|<xref:System.Activities.Statements.State.Exit%2A>|错误|指定在从此状态转换时发生的操作。 展开 <xref:System.Activities.Statements.State> 活动时，可以通过从“工具箱”拖动某个活动并将其放置到状态的“退出”部分来设置此值 。|
|<xref:System.Activities.Statements.State.Transitions%2A>|错误|列出源自 <xref:System.Activities.Statements.State> 的可能转换。 列表中的每个项有一个指向关联的 <xref:System.Activities.Statements.Transition> 和目标 <xref:System.Activities.Statements.State> 的链接。 单击此链接会将设计器切换到 <xref:System.Activities.Statements.Transition> 或 <xref:System.Activities.Statements.State> 的扩展视图。|

## <a name="see-also"></a>另请参阅

- [StateMachine](../workflow-designer/statemachine-activity-designer.md)
- [FinalState](../workflow-designer/finalstate-activity-designer.md)
- [过渡](../workflow-designer/transition-activity-designer.md)
