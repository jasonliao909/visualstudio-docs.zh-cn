---
title: 工作流设计器活动设计器
description: 了解 While 活动如何在指定条件的计算结果为 true 的情况下执行其主体中包含的活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.While.UI
ms.assetid: ea008091-2e4c-4f64-bfa5-afb919552446
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: f55218e75f887d8fa3d16213fd3cbc9adbb09b43a5404826bc7c2d6d055e9ab7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121365829"
---
# <a name="while-activity-designer"></a>While 活动设计器

<xref:System.Activities.Statements.While> <xref:System.Activities.Statements.While.Body%2A> 当指定的 <xref:System.Activities.Statements.While.Condition%2A> 计算结果为 **true** 时，活动执行在其中包含的活动。 包含的活动可能永远都不会执行。 如果希望所包含的活动至少执行一次，请改用 <xref:System.Activities.Statements.DoWhile> 活动。

## <a name="while-properties-in-workflow-designer"></a>工作流设计器中的 While 属性

下表列出最有用的 <xref:System.Activities.Statements.While> 活动属性并说明如何在设计器中使用它们。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.While> 活动设计器在标头中的友好名称。 默认值为 While。 该值可以在 " **属性** " 窗口中编辑，也可以直接在活动设计器标头中编辑。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.While.Body%2A>|错误|包含 <xref:System.Activities.Statements.While.Condition%2A> 计算结果为 **true** 时要执行的活动。|
|<xref:System.Activities.Statements.While.Condition%2A>|正确|包含计算以确定是否要执行中的活动的 Visual Basic 表达式 <xref:System.Activities.Statements.While.Body%2A> 。|

## <a name="see-also"></a>请参阅

- [控制流](../workflow-designer/control-flow-activity-designers.md)
- [DoWhile](../workflow-designer/dowhile-activity-designer.md)
