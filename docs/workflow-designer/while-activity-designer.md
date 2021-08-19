---
title: 工作流设计器 - While 活动设计器
description: 了解 While 活动如何执行其 Body 中包含的活动，而指定的 Condition 计算结果为 true。
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
ms.openlocfilehash: f7d5859ae9841eff105b7a18f5f4730d440df94f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122098874"
---
# <a name="while-activity-designer"></a>While 活动设计器

活动 <xref:System.Activities.Statements.While> 执行 其 中包含的活动， <xref:System.Activities.Statements.While.Body%2A> 而指定的 <xref:System.Activities.Statements.While.Condition%2A> 计算结果为 **true。** 包含的活动可能永远都不会执行。 如果希望所包含的活动至少执行一次，请改用 <xref:System.Activities.Statements.DoWhile> 活动。

## <a name="while-properties-in-workflow-designer"></a>工作流设计器中的 While 属性

下表列出最有用的 <xref:System.Activities.Statements.While> 活动属性并说明如何在设计器中使用它们。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.While> 活动设计器在标头中的友好名称。 默认值为 While。 可以在"属性"窗口中编辑 **该值，也可以** 直接在活动设计器标头上编辑该值。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.While.Body%2A>|错误|包含计算结果为 true 时 <xref:System.Activities.Statements.While.Condition%2A> 要 **执行的活动**。|
|<xref:System.Activities.Statements.While.Condition%2A>|正确|包含Visual Basic一个表达式，该表达式计算该表达式确定是否要执行 <xref:System.Activities.Statements.While.Body%2A> 中的活动。|

## <a name="see-also"></a>请参阅

- [控制流](../workflow-designer/control-flow-activity-designers.md)
- [DoWhile](../workflow-designer/dowhile-activity-designer.md)
