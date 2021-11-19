---
title: 工作流设计器 - StateMachine 活动设计器
description: 了解 StateMachine 活动如何包含使用熟悉的状态机范式的状态和模型工作流的集合。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- StateMachine Designer
- System.Activities.Statements.StateMachine.UI
ms.assetid: 474d5fb3-1049-4b3f-bc6b-7524dbbe1672
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: b6982a3875bc09e95b6f33dd30010adf029b3a91
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664909"
---
# <a name="statemachine-activity-designer"></a>StateMachine 活动设计器

<xref:System.Activities.Statements.StateMachine> 活动包含使用熟悉的状态机范式的状态和模型工作流的集合。

## <a name="using-the-statemachine-activity-designer"></a>使用 StateMachine 活动设计器

若要添加 <xref:System.Activities.Statements.StateMachine> 活动，请将“StateMachine”活动设计器从“工具箱”的“状态机”部分拖到“工作流设计器”图面  。 若要将子状态添加到此 <xref:System.Activities.Statements.StateMachine> 活动，请将 <xref:System.Activities.Statements.State> 或 <xref:System.Activities.Core.Presentation.FinalState> 从“工具箱”拖放到“StateMachine” 。

### <a name="statemachine-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 StateMachine 活动属性

下表列出可使用工作流设计器设置的 <xref:System.Activities.Statements.StateMachine> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.StateMachine> 活动设计器在标头中的友好名称。 默认值为“StateMachine”。 可以在属性网格或直接在活动设计器的标头中编辑该值。 <xref:System.Activities.Activity.DisplayName%2A> 用于痕迹导航，后者显示在工作流设计器顶部。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|

## <a name="see-also"></a>另请参阅

- [流程图](../workflow-designer/flowchart-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)
