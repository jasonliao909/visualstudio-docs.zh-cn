---
title: 工作流设计器 - FinalState 活动设计器
description: 了解如何使用 FinalState 设计器创建终止状态机实例的 State。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: aa186893-8775-40dd-981f-8593ead831d0
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: a44cf8413e60b0dd5049f7ce31d699e6cfbbca47
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665664"
---
# <a name="finalstate-activity-designer"></a>FinalState 活动设计器

<xref:System.Activities.Core.Presentation.FinalState> 设计器用于创建终止状态机实例的 <xref:System.Activities.Statements.State>。

## <a name="using-the-finalstate-activity-designer"></a>使用 FinalState 活动设计器

“FinalState”设计器用于创建在状态机中预配置为“正在终止”状态的 <xref:System.Activities.Statements.State>。 使用 <xref:System.Activities.Core.Presentation.FinalState> 活动设计器创建的 <xref:System.Activities.Statements.State> 具有设置为“true”的 <xref:System.Activities.Statements.State.IsFinal%2A> 属性，没有 <xref:System.Activities.Statements.State.Exit%2A> 活动，也没有源自它的转换。 要使用 <xref:System.Activities.Core.Presentation.FinalState> 活动设计器添加在状态机中预配置为“正在终止”状态的 <xref:System.Activities.Statements.State> 活动，请将“FinalState”活动设计器从“工具箱”的“状态机”部分拖放到工作流设计器上  。 <xref:System.Activities.Core.Presentation.FinalState> 活动设计器可以放置到 <xref:System.Activities.Statements.StateMachine> 上，以后可添加转换；或在删除 <xref:System.Activities.Core.Presentation.FinalState> 活动设计器时可创建转换。 若要详细了解如何创建转换，请参阅[转换](../workflow-designer/transition-activity-designer.md)。

### <a name="state-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 State 活动属性

下表列出可使用 <xref:System.Activities.Core.Presentation.FinalState> 设计器设置的属性并说明如何在设计器中使用它们。 其中一些属性可以在属性网格中进行编辑，另一些属性可以在设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Statements.State.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.State> 活动设计器在标头中的友好名称。 默认值为“State”。 可以在属性网格或直接在活动设计器的标头中编辑该值。 <xref:System.Activities.Statements.State.DisplayName%2A> 用于痕迹导航，后者显示在工作流设计器顶部。<br /><br /> 虽然 <xref:System.Activities.Statements.State.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.State.Entry%2A>|错误|指定在转换到此状态时发生的操作。 可以通过将活动从“工具箱”拖放到状态的 <xref:System.Activities.Statements.State.Entry%2A> 部分来设置此值。|

## <a name="see-also"></a>另请参阅

- [StateMachine](../workflow-designer/statemachine-activity-designer.md)
- [State](../workflow-designer/state-activity-designer.md)
- [过渡](../workflow-designer/transition-activity-designer.md)