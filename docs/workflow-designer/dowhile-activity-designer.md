---
title: 工作流设计器 - DoWhile 活动设计器
description: 了解 DoWhile 活动如何至少执行一次其 Body 中包含的活动，直到指定条件的计算结果为 false。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.DoWhile.UI
ms.assetid: 948deb35-d72f-462b-bea6-4b119c10a148
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 942552f127cebaff4c0f923118fb8be0ac9b141a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602189"
---
# <a name="dowhile-activity-designer"></a>DoWhile 活动设计器

<xref:System.Activities.Statements.DoWhile> 活动至少执行一次其 <xref:System.Activities.Statements.DoWhile.Body%2A> 中包含的活动，直到指定条件的计算结果为 false。 如果需要执行循环体中包含的活动零次或多次，请改用 <xref:System.Activities.Statements.While> 活动。

## <a name="dowhile-properties-in-the-workflow-designer"></a>工作流设计器中的 DoWhile 属性

下表列出了最有用处的 <xref:System.Activities.Statements.DoWhile> 活动属性，并说明了如何在设计器中使用它们：

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Statements.DoWhile.Body%2A>|错误|当条件为 true 时要执行的活动。 若要添加 <xref:System.Activities.Statements.DoWhile.Body%2A> 活动，请将活动从工具箱拖放到“DoWhile”活动设计器上带提示文本“在此处放置活动”的“Body”框中。|
|<xref:System.Activities.Statements.DoWhile.Condition%2A>|True|每次循环迭代后要计算的条件。 若要设置 <xref:System.Activities.Statements.DoWhile.Condition%2A>，请在“DoWhile”活动设计器或属性网格中的“Condition”框中键入 Visual Basic 表达式。|

## <a name="see-also"></a>另请参阅

- [While](../workflow-designer/while-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)