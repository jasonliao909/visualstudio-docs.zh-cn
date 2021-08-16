---
title: 工作流设计器 FinalState 活动设计器
description: 了解如何使用 FinalState 设计器创建终止状态机实例的状态。
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
ms.openlocfilehash: e51fd5a806a9ede74d824c94d3eda84dc0541e9ebe235cb76242c6a783d02c9a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121423704"
---
# <a name="finalstate-activity-designer"></a>FinalState 活动设计器

<xref:System.Activities.Core.Presentation.FinalState> 设计器用于创建终止状态机实例的 <xref:System.Activities.Statements.State>。

## <a name="using-the-finalstate-activity-designer"></a>使用 FinalState 活动设计器

**FinalState** 设计器用于创建在 <xref:System.Activities.Statements.State> 状态机中预配置为终止状态的。 <xref:System.Activities.Statements.State>使用 <xref:System.Activities.Core.Presentation.FinalState> 活动设计器创建的会将其 <xref:System.Activities.Statements.State.IsFinal%2A> 属性设置为 **true**，没有 <xref:System.Activities.Statements.State.Exit%2A> 活动，也没有来自它的转换。 若要使用 <xref:System.Activities.Core.Presentation.FinalState> 活动设计器来添加在 <xref:System.Activities.Statements.State> 状态机中预配置为终止状态的活动，请将 " **FinalState** " 活动设计器从 "**工具箱**" 的 "**状态机**" 部分拖放到工作流设计器上。 <xref:System.Activities.Core.Presentation.FinalState> 活动设计器可以放置到 <xref:System.Activities.Statements.StateMachine> 上，以后可添加转换；或在删除 <xref:System.Activities.Core.Presentation.FinalState> 活动设计器时可创建转换。 有关创建转换的详细信息，请参阅 [转换](../workflow-designer/transition-activity-designer.md)。

### <a name="state-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 State 活动属性

下表列出可使用 <xref:System.Activities.Core.Presentation.FinalState> 设计器设置的属性并说明如何在设计器中使用它们。 其中一些属性可以在属性网格中进行编辑，另一些属性可以在设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Statements.State.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.State> 活动设计器在标头中的友好名称。 默认值为 " **状态**"。 可以在属性网格或直接在活动设计器的标头中编辑该值。 <xref:System.Activities.Statements.State.DisplayName%2A> 用于痕迹导航，后者显示在工作流设计器顶部。<br /><br /> 虽然 <xref:System.Activities.Statements.State.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.State.Entry%2A>|错误|指定在转换到此状态时发生的操作。 可以通过将某个活动从 " **工具箱** " 拖放到状态的部分来设置此值 <xref:System.Activities.Statements.State.Entry%2A> 。|

## <a name="see-also"></a>请参阅

- [StateMachine](../workflow-designer/statemachine-activity-designer.md)
- [State](../workflow-designer/state-activity-designer.md)
- [过渡](../workflow-designer/transition-activity-designer.md)