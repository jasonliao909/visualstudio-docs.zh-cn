---
title: 工作流设计器 - 选取活动设计器
description: 了解 Pick 活动如何提供基于事件的控制流并执行多个分支之一以响应触发事件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Pick.UI
ms.assetid: 642c0a47-1b47-45de-a19a-ca0606cedd7a
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: e871e38cb9f675e1a76edae0410cbd5ac45aee10
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664676"
---
# <a name="pick-activity-designer"></a>Pick 活动设计器

<xref:System.Activities.Statements.Pick> 活动提供基于事件的控制流。 该活动执行多个分支中的一个分支来响应某个触发的事件。

## <a name="the-pick-activity"></a>Pick 活动

<xref:System.Activities.Statements.Pick> 活动包含一个 <xref:System.Activities.Statements.PickBranch> 对象的集合，<xref:System.Activities.Statements.Pick> 活动会由于某些作为触发器的传入事件而执行其中一个对象。 这样，工作流设计器基于事件的控制流建模。 每个 <xref:System.Activities.Statements.PickBranch> 都包含一个 <xref:System.Activities.Statements.PickBranch.Trigger%2A> 和一个 <xref:System.Activities.Statements.PickBranch.Action%2A>。 在活动执行 <xref:System.Activities.Statements.Pick> 开始时，将计划元素的所有 <xref:System.Activities.Statements.PickBranch> 触发器活动。 在第一个活动完成之后，安排其相应的操作活动，并且取消所有其他触发器活动。

### <a name="how-to-use-the-pick-activity-designer"></a>如何使用 Pick 活动设计器

访问 **"工具箱**"的"控件 **Flow"类别中** 的"选取"**活动设计器**。 可以将 **Pick** 活动设计器从"工具箱"拖动到工作流设计器放置活动设计器的位置（例如，在序列活动设计器内部）拖放到"对象"图面上。  在将活动工作流设计器，它会创建一个 活动，默认情况下，该活动包含两个空活动作为显示名称为 Branch1 和 <xref:System.Activities.Statements.Pick> <xref:System.Activities.Statements.PickBranch> Branch2 的元素。 可以在 <xref:System.Activities.Statements.PickBranch.DisplayName%2A> **PickBranch** 活动设计器标头或每个分支的"属性 **"** 窗口中编辑这些各自的属性值。

有两种方法可以将活动添加到 对象的集合：从"工具箱"拖放 <xref:System.Activities.Statements.PickBranch> <xref:System.Activities.Statements.Pick> **PickBranch** 设计器，或者使用"选取"设计图面中的右键单击菜单。 有关详细信息，请参阅 [PickBranch](../workflow-designer/pickbranch-activity-designer.md) 主题。 请注意，可以在 Pick 活动设计器中 **放置的唯一** 项是 **PickBranch** 活动设计器。

### <a name="pick-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 Pick 活动属性

下表列出 <xref:System.Activities.Statements.Pick> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.Pick> 活动设计器在标头中的友好名称。 默认值为 Pick。 可以在属性网格或直接在活动设计器的标头中编辑该值。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|

## <a name="see-also"></a>另请参阅

- [控制流](../workflow-designer/control-flow-activity-designers.md)
- [Pick 活动](/dotnet/framework/windows-workflow-foundation/pick-activity)
- [使用 Pick 活动](/dotnet/framework/windows-workflow-foundation/samples/using-the-pick-activity)