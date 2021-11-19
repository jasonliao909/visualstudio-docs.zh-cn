---
title: 工作流设计器 - Sequence 活动设计器
description: 了解 Sequence 活动如何包含其按顺序执行的已排序的子活动集合。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Sequence.UI
ms.assetid: 51c8d3cb-4d43-458f-9631-b63755f9ac94
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 7980e01f23dab3ddb927af207e4e2ce67ab515a7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666106"
---
# <a name="sequence-activity-designer"></a>Sequence 活动设计器

<xref:System.Activities.Statements.Sequence> 活动包含子活动的已排序集合，将按该排序执行这些子活动。

按顺序执行一组活动的另一个方法是使用 <xref:System.Activities.Statements.Flowchart> 活动。 当你具有简单的分支或循环程序流并且希望通过图解法建模时，请考虑使用[流程图](../workflow-designer/flowchart-activity-designer.md)。

## <a name="using-the-sequence-activity-designer"></a>使用 Sequence 活动设计器

若要添加 <xref:System.Activities.Statements.Sequence> 活动，请将“Sequence”活动设计器从“工具箱”拖到“工作流设计器”图面上 。 若要向此 <xref:System.Activities.Statements.Sequence> 活动添加子活动，请将一些其他活动从“工具箱”拖放到带提示文本“在此处放置活动”的框中的三角形上。

### <a name="sequence-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 Sequence 活动属性

下表列出 <xref:System.Activities.Statements.Sequence> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.Sequence> 活动设计器在标头中的友好名称。 默认值为 Sequence。 可以在属性网格或直接在活动设计器的标头中编辑该值。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|

## <a name="see-also"></a>另请参阅

- [流程图](../workflow-designer/flowchart-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)