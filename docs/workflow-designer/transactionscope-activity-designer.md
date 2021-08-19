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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122114506"
---
# <a name="transactionscope-activity-designer"></a>TransactionScope 活动设计器

**TransactionScope** 活动设计器用于创建和配置 <xref:System.Activities.Statements.TransactionScope> 活动。

## <a name="the-transactionscope-activity"></a>TransactionScope 活动

<xref:System.Activities.Statements.TransactionScope> 活动在单个事务中执行所包含的活动。 在 <xref:System.Activities.Statements.TransactionScope.Body%2A> 活动以及该事务中的所有其他参与者成功完成时将提交该事务。

### <a name="using-the-transactionscope-activity-designer"></a>使用 TransactionScope 活动设计器

访问" **工具箱"** 的"事务 **"类别中的** TransactionScope 活动 **设计器**。 可以将 **TransactionScope** 活动设计器从"工具箱"拖动到工作流设计器放置活动的位置（例如 位于 内）上 <xref:System.Activities.Statements.Sequence> 。 这将创建具有 TransactionScope 的默认 <xref:System.Activities.Statements.TransactionScope> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 可以在 TransactionScope 活动设计器的标头或属性网格的 <xref:System.Activities.Activity.DisplayName%2A> **DisplayName** 框中编辑该值。

### <a name="the-transactionscope-properties"></a>TransactionScope 属性

下表列出 <xref:System.Activities.Statements.TransactionScope> 属性并说明如何在设计器中使用它们。 可以在 <xref:System.Activities.Activity.DisplayName%2A> <xref:System.Activities.Statements.TransactionScope.Body%2A> 图面上编辑 和 工作流设计器属性。 但其他属性必须在属性网格上编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.TransactionScope> 活动的可选友好名称。 默认值为 TransactionScope。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.TransactionScope.Body%2A>|正确|指定要在单个事务中执行的活动。 若要添加活动，请从"工具箱"将活动拖放到 TransactionScope 活动设计器上的"正文"框中，提示 <xref:System.Activities.Statements.TransactionScope.Body%2A> 文本为"此处放置活动"。   |
|<xref:System.Activities.Statements.TransactionScope.IsolationLevel%2A>|True|指定此 <xref:System.Transactions.IsolationLevel> 的 <xref:System.Activities.Statements.TransactionScope>。|
|<xref:System.Activities.Statements.TransactionScope.Timeout%2A>|错误|指定必须在其间完成事务的时间间隔（格式为 00:00:00，表示小时:分钟:秒）。 默认值为 1 分钟 (00:01:00)。|
|<xref:System.Activities.Statements.TransactionScope.AbortInstanceOnTransactionFailure*>|正确|指定指示在事务中止的情况下是否应中止工作流的值。|

## <a name="see-also"></a>请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [TerminateWorkflow](../workflow-designer/terminateworkflow-activity-designer.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [确认](../workflow-designer/confirm-activity-designer.md)
