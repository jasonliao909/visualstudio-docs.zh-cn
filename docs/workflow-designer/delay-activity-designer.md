---
title: 工作流设计器 - 延迟活动设计器
description: 了解延迟活动，以及如何使用 Delay 活动设计器创建和配置 Delay 活动。
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
ms.openlocfilehash: 2d59f0db70804049a0392350942000d4331715021fb30f7ab43183d7326d02f4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121440534"
---
# <a name="delay-activity-designer"></a>Delay 活动设计器

Delay 活动设计器用于创建和配置 <xref:System.Activities.Statements.Delay> 活动。

## <a name="the-delay-activity"></a>Delay 活动

<xref:System.Activities.Statements.Delay> 活动可将工作流的执行延迟指定时长。

### <a name="use-the-delay-activity-designer"></a>使用 Delay 活动设计器

可以在 **"** 工具箱"的"基元"类别中找到"延迟"活动设计器，单击"工具箱"的"工具箱"选项卡即可工作流设计器。  或者，从"视图 **"菜单中** 选择"**工具箱"，** 或按 **Ctrl** + **Alt** + **X**。

可以将 **Delay** 活动设计器从"工具箱"拖动到工作流设计器放置活动（例如位于 内）的"延迟"图面 <xref:System.Activities.Statements.Sequence> 。 删除活动设计器会创建 <xref:System.Activities.Statements.Delay> 默认为 Delay <xref:System.Activities.Activity.DisplayName%2A> 的活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在 Delay 活动设计器的标头或属性网格的 **DisplayName** 框中编辑 。

### <a name="the-delay-properties"></a>Delay 属性

下表显示了 <xref:System.Activities.Statements.Delay> 属性，并介绍了如何在设计器中使用这些属性。 这些属性可以在属性网格中编辑，其中一些属性可以在工作流设计器编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.Delay> 活动的友好名称。 默认值为 Delay。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值并非严格要求，但最佳做法是使用值。|
|<xref:System.Activities.Statements.Delay.Duration%2A>|正确|将工作流延迟的时长。 此属性在属性网格中设置。 键入 00:00:00 格式的文本 <xref:System.TimeSpan> 或 Visual Basic 表达式来指定时长。|

## <a name="see-also"></a>另请参阅

- [基元](../workflow-designer/primitives-activity-designers.md)
- [Assign](../workflow-designer/assign-activity-designer.md)
- [Delay 活动设计器](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)