---
title: 工作流设计器-If 活动设计器
description: 了解 If 活动如何计算条件并根据该计算结果执行活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.If.UI
ms.assetid: 930a8fa2-db98-43e9-ad6d-a85cc7a6519a
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: f353cb3f301d09fe5434fd12deaa620b5f0c4ddfe38ca7a82d1d2e9a30f2e8c3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121243401"
---
# <a name="if-activity-designer"></a>If 活动设计器

<xref:System.Activities.Statements.If> 活动计算条件并根据该计算结果执行活动。 当使用编程的过程建模样式时，此活动最有用。 例如，<xref:System.Activities.Statements.If> 活动可嵌套在 <xref:System.Activities.Statements.Sequence> 活动或 <xref:System.Activities.Statements.Parallel> 活动内。 如果您使用的是 <xref:System.Activities.Statements.Flowchart> 活动，请考虑改用 <xref:System.Activities.Statements.FlowDecision> 活动。

## <a name="if-properties-in-the-workflow-designer"></a>工作流设计器中的 If 属性

下表列出最有用的 <xref:System.Activities.Statements.If> 活动属性并说明如何在设计器中使用它们。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Statements.If.Condition%2A>|正确|用于确定要执行哪个子活动的条件。 若要设置 <xref:System.Activities.Statements.If.Condition%2A> ，请在 " **If** " 活动设计器或属性网格中的 "**条件**" 框中键入 Visual Basic 表达式。|
|<xref:System.Activities.Statements.If.Else%2A>|错误|为 false 时要执行的 <xref:System.Activities.Statements.If.Condition%2A> 活动。 若要添加由分支执行的活动 <xref:System.Activities.Statements.If.Else%2A> ，请将活动从 "**工具箱**" 拖放到 " **If** " 活动设计器上带提示文本 "在此处放置活动" 的 " **Else** " 框中。|
|<xref:System.Activities.Statements.If.Then%2A>|错误|如果为 true，则为要执行的活动 <xref:System.Activities.Statements.If.Condition%2A> 。  若要添加由分支执行的活动 <xref:System.Activities.Statements.If.Then%2A> ，请将活动从 "**工具箱**" 拖放到 " **If** " 活动设计器上带有提示文本 "将活动放置到此处" 的 " **Then** " 框中。|

## <a name="see-also"></a>请参阅

- [序列](../workflow-designer/sequence-activity-designer.md)
- [Parallel](../workflow-designer/parallel-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)
