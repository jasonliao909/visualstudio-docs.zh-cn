---
title: 工作流设计器 - TransactionScope 活动设计器
description: 了解如何使用 TransactionScope 活动设计器创建和配置 TransactionScope 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.TransactionScope.UI
ms.assetid: 8d7ebfc6-7478-4888-b3b0-b14f296096af
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: d3d84514690c4f2a00caea3b88946ffbd4da7cbc
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664902"
---
# <a name="transactionscope-activity-designer"></a>TransactionScope 活动设计器

TransactionScope 活动设计器用于创建和配置 <xref:System.Activities.Statements.TransactionScope> 活动。

## <a name="the-transactionscope-activity"></a>TransactionScope 活动

<xref:System.Activities.Statements.TransactionScope> 活动在单个事务中执行所包含的活动。 在 <xref:System.Activities.Statements.TransactionScope.Body%2A> 活动以及该事务中的所有其他参与者成功完成时将提交该事务。

### <a name="using-the-transactionscope-activity-designer"></a>使用 TransactionScope 活动设计器

访问 TransactionScope 活动设计器，其位于工具箱的“事务”类别中  。 可以将“TransactionScope”活动设计器从“工具箱”拖放到工作流设计器图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内 。 这将创建具有 TransactionScope 的默认 <xref:System.Activities.Statements.TransactionScope> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 可以在“TransactionScope”活动设计器的标头中或在属性网格的“DisplayName”框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值 。

### <a name="the-transactionscope-properties"></a>TransactionScope 属性

下表列出 <xref:System.Activities.Statements.TransactionScope> 属性并说明如何在设计器中使用它们。 可在工作流设计器图面上编辑 <xref:System.Activities.Activity.DisplayName%2A> 和 <xref:System.Activities.Statements.TransactionScope.Body%2A> 属性。 但其他属性必须在属性网格上编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.TransactionScope> 活动的可选友好名称。 默认值为 TransactionScope。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.TransactionScope.Body%2A>|True|指定要在单个事务中执行的活动。 若要添加 <xref:System.Activities.Statements.TransactionScope.Body%2A> 活动，请将活动从“工具箱”放置到“TransactionScope”活动设计器上带提示文本“在此处放置活动”的“Body”框中  。|
|<xref:System.Activities.Statements.TransactionScope.IsolationLevel%2A>|True|指定此 <xref:System.Transactions.IsolationLevel> 的 <xref:System.Activities.Statements.TransactionScope>。|
|<xref:System.Activities.Statements.TransactionScope.Timeout%2A>|错误|指定必须在其间完成事务的时间间隔（格式为 00:00:00，表示小时:分钟:秒）。 默认值为 1 分钟 (00:01:00)。|
|<xref:System.Activities.Statements.TransactionScope.AbortInstanceOnTransactionFailure*>|True|指定指示在事务中止的情况下是否应中止工作流的值。|

## <a name="see-also"></a>另请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [TerminateWorkflow](../workflow-designer/terminateworkflow-activity-designer.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [确认](../workflow-designer/confirm-activity-designer.md)
