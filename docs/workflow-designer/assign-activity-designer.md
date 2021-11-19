---
title: 工作流设计器 - Assign 活动设计器
description: 了解如何使用 Assign 活动设计器创建和配置 Assign 活动，以及 Assign 活动如何将值分配给变量或参数。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Assign.UI
ms.assetid: ba3feb3c-f144-47ea-926d-cf752b804153
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 524d55608b8cc75deea1c876ab03a4a437ad2049
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126667597"
---
# <a name="assign-activity-designer"></a>Assign 活动设计器

“Assign”活动设计器用于创建和配置 <xref:System.Activities.Statements.Assign> 活动。

## <a name="the-assign-activity"></a>Assign 活动

<xref:System.Activities.Statements.Assign> 活动为变量或自变量赋值。

### <a name="using-the-assign-activity-designer"></a>使用 Assign 活动设计器

“Assign”活动设计器可在“工具箱”的“基元”类别中找到，“工具箱”可通过单击“工具箱”选项卡（或者，从“视图”菜单中选择“工具箱”或按 CTRL+ALT+X）来访问。     

可以将“Assign”活动设计器从“工具箱”拖放到工作流设计器图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内。  删除“Assign”活动设计器将创建一个 <xref:System.Activities.Statements.Assign> 活动，其默认的”DisplayName”为“Assign”。  可以在“Assign”活动设计器的标头中或在属性网格的“DisplayName”框中编辑 <xref:System.Activities.Activity.DisplayName%2A>。 

### <a name="the-assign-properties"></a>Assign 属性

下表列出 <xref:System.Activities.Statements.Assign> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在工作流设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.Assign> 活动的友好名称。 默认值为 Assign。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.Assign.To%2A>|True|为其赋 <xref:System.Activities.Statements.Assign.Value%2A> 的变量或自变量。 该值必须是有效的 Visual Basic 标识符。 若要设置该属性，请在“Assign”活动设计器或属性网格中的“To”框中键入 Visual Basic 表达式。 |
|<xref:System.Activities.Statements.Assign.Value%2A>|True|赋给变量的值。 若要设置 <xref:System.Activities.Statements.Assign.Value%2A>，请在“Assign”活动设计器或属性网格中的“值”框中键入 Visual Basic 表达式。 |

## <a name="see-also"></a>另请参阅

- [基元](../workflow-designer/primitives-activity-designers.md)
- [延迟](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)