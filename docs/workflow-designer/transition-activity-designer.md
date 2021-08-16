---
title: 工作流设计器 - 转换活动设计器
description: 了解如何使用转换活动设计器配置两种状态之间的转换。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Transition.UI
ms.assetid: f6e8b5cc-7fb8-4699-9703-f3c9fc7cc316
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 7d7eed0579541f8f0e5355719c8bb2d2b79190854ea288b887af0000bcd370e3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121393414"
---
# <a name="transition-activity-designer"></a>事务活动设计器

<xref:System.Activities.Statements.Transition> 表示两个状态间的转换。

## <a name="using-the-transition-activity-designer"></a>使用 Transition 活动设计器

Transition 活动设计器允许您在两个状态之间配置转换。

### <a name="transition-properties-in-the-workflow-designer"></a>工作流设计器中的 Transition 属性

下表列出可使用工作流设计器设置的 <xref:System.Activities.Statements.Transition> 属性并说明如何在设计器中使用它们。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Statements.Transition.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.Transition> 活动设计器的友好名称。 默认值为 **T1**。 可在属性网格、扩展转换设计器的标题以及扩展转换设计器内的操作部分的标题中编辑值。 <xref:System.Activities.Activity.DisplayName%2A> 用于痕迹导航，后者显示在工作流设计器顶部。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.Transition.Condition%2A>|错误|如果存在，则指定一个表达式，该表达式在将控件传递给目标状态之前，必须计算结果为 True。 可以在属性网格和扩展转换设计器中编辑此条件。 共享转换中的多个条件按显示在转换设计器中的顺序进行评估。 **注意：** 请注意，如果转换的 计算结果为 False (或者共享触发器转换的所有条件评估为 False) ，则转换不会发生，并且将重新计划从状态进行的所有转换的所有 <xref:System.Activities.Statements.Transition.Condition%2A> 触发器。 在本教程中，由于配置条件的方式，这种情况不会发生（我们针对猜测是正确或者错误提供了具体的操作）。|
|**Source**|正确|指示源自此转换的状态。 单击源状态的名称可将设计器视图切换到状态的扩展视图。 在创建转换时设置此值，并且不能更改它。|
|<xref:System.Activities.Statements.Transition.Trigger%2A>|错误|指定其完成启动转换的活动。 若要设置此活动，请将活动从"工具箱 **"** 拖动到转换 **的"触发器** "部分。|
|<xref:System.Activities.Statements.Transition.Action%2A>|错误|指定在触发器活动完成时执行的活动，如果存在 ，则 <xref:System.Activities.Statements.Transition.Condition%2A> 计算结果为 **true。** 在源状态的 <xref:System.Activities.Statements.State.Exit%2A> 活动后、转换到目标状态时执行此活动，如果存在，则执行。 展开转换设计器时，可以通过从"工具箱"拖动活动，将其拖放到转换的"操作 **"部分来** 设置此值。 单个转换可对应多个操作。 可以展开和收缩各个操作，在转换中存在多个操作时可通过单击在操作上显示的向上或向下箭头键进行排序。|
|**目标**|正确|指示转换完成后状态计算机转换到的状态。 这与对象模型中转换的 <xref:System.Activities.Statements.Transition.To%2A> 属性相对应。 单击目标状态的名称可将设计器视图切换到状态的扩展视图。 在创建转换时设置此值，并可以通过拖动将转换连接到设计器中的目标状态的箭头进行更改。|

### <a name="creating-transitions"></a>创建转换

通过将某行从一个状态拖到另一个状态，或在从一个状态拖动到另一个状态时通过将状态拖放到出现的三角形上，来创建转换。 若要通过拖动来创建转换，请将鼠标悬停在源状态的边缘，并将某行从源状态拖到目标状态。 若要通过拖放方式创建转换，请拖动目标状态并将其悬停在源状态，将它拖到源状态周围显示的四个三角形之一。 目标状态可以是从"工具箱"拖动的新状态，或者是从工作流设计器拖动的现有状态。

> [!NOTE]
> 状态机中的单个状态使用工作流设计器可以创建多达 76 个转换。 对在设计器外创建的工作流状态的转换限制只受系统资源限制。

共享触发器转换是共享相同的触发事件的一组转换。 共享触发器基于为共享公用触发器事件的多个转换配置的表达式评估结果，允许有条件转换到目标状态。 若要将其他操作添加到转换和创建共享转换，请单击指示所需转换的开始的圆并将它拖到所需的状态。 新转换将与初始转换共享相同的触发器，但它将具有一个唯一的条件和操作。 也可以从转换设计器内部创建共享转换，方法是单击转换设计器底部的"添加共享触发器转换"，然后从"可用状态"下拉列表中选择所需的目标状态。 

## <a name="see-also"></a>另请参阅

- [StateMachine](../workflow-designer/statemachine-activity-designer.md)
- [FinalState](../workflow-designer/finalstate-activity-designer.md)
- [State](../workflow-designer/state-activity-designer.md)
