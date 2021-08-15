---
title: 工作流设计器 - StateMachine 活动设计器
description: 了解 StateMachine 活动如何使用熟悉的状态机范例包含状态集合并模型工作流。
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
ms.openlocfilehash: ca75e366d1c7e8c14b5bc59b0155cb99aabaf76464460226526979a42d54ed5f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121440404"
---
# <a name="statemachine-activity-designer"></a>StateMachine 活动设计器

<xref:System.Activities.Statements.StateMachine> 活动包含使用熟悉的状态机范式的状态和模型工作流的集合。

## <a name="using-the-statemachine-activity-designer"></a>使用 StateMachine 活动设计器

若要添加 <xref:System.Activities.Statements.StateMachine> 活动，请将 **StateMachine** 活动设计器从"工具箱"的"状态机"部分拖放到工作流设计器图面。 若要向此活动添加子状态，请从"工具箱"拖动 或 <xref:System.Activities.Statements.StateMachine> <xref:System.Activities.Statements.State> <xref:System.Activities.Core.Presentation.FinalState> 并将其拖放到 **StateMachine 上**。 

### <a name="statemachine-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 StateMachine 活动属性

下表列出可使用工作流设计器设置的 <xref:System.Activities.Statements.StateMachine> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.StateMachine> 活动设计器在标头中的友好名称。 默认值为 **StateMachine**。 可以在属性网格或直接在活动设计器的标头中编辑该值。 <xref:System.Activities.Activity.DisplayName%2A> 用于痕迹导航，后者显示在工作流设计器顶部。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|

## <a name="see-also"></a>另请参阅

- [流程图](../workflow-designer/flowchart-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)
