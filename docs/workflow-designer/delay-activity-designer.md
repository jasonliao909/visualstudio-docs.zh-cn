---
title: 工作流设计器 - Delay 活动设计器
description: 了解 Delay 活动，以及如何使用 Delay 活动设计器创建和配置 Delay 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Delay.UI
ms.assetid: f51742a8-2c9a-47d1-8a23-18459d03ae19
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 71618b2ebbd0abc6f089ad9838942a99d0897e7c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666985"
---
# <a name="delay-activity-designer"></a>Delay 活动设计器

“Delay”活动设计器用于创建和配置 <xref:System.Activities.Statements.Delay> 活动。

## <a name="the-delay-activity"></a>Delay 活动

<xref:System.Activities.Statements.Delay> 活动可将工作流的执行延迟指定时长。

### <a name="use-the-delay-activity-designer"></a>使用 Delay 活动设计器

可以在“工具箱”的“Primitives”类别中找到“Delay”活动设计器，通过单击工作流设计器的“工具箱”选项卡来访问   。 或者，从“视图”菜单栏中选择“工具箱”或按 Ctrl+Alt+X    。

可以将 Delay 活动设计器从“工具箱”拖放到工作流设计器图面上通常放置活动的任意位置，如 <xref:System.Activities.Statements.Sequence> 内 。 删除活动设计器将创建一个 <xref:System.Activities.Statements.Delay> 活动，其默认 <xref:System.Activities.Activity.DisplayName%2A> 为 Delay。 可以在 “Delay”活动设计器的标头中或在属性网格的“DisplayName”框中编辑 <xref:System.Activities.Activity.DisplayName%2A>。

### <a name="the-delay-properties"></a>Delay 属性

下表显示 <xref:System.Activities.Statements.Delay> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在工作流设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.Delay> 活动的友好名称。 默认值为 Delay。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.Delay.Duration%2A>|True|将工作流延迟的时长。 此属性在属性网格中设置。 键入 00:00:00 格式的文本 <xref:System.TimeSpan> 或 Visual Basic 表达式来指定时长。|

## <a name="see-also"></a>另请参阅

- [基元](../workflow-designer/primitives-activity-designers.md)
- [Assign](../workflow-designer/assign-activity-designer.md)
- [Delay 活动设计器](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)