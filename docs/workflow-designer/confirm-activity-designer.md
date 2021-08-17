---
title: 工作流设计器 - 确认活动设计器
description: 了解 Confirm 活动设计器，以及如何使用此设计器创建和配置 Confirm 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Confirm.UI
ms.assetid: c753b67b-b0e7-462a-bb4e-ba8db04a078d
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 017a89d2e68e3d466f7625c8dbb2312d450f888c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122045874"
---
# <a name="confirm-activity-designer"></a>Confirm 活动设计器

**Confirm** 活动设计器用于创建和配置 <xref:System.Activities.Statements.Confirm> 活动。

## <a name="the-confirm-activity"></a>Confirm 活动
 <xref:System.Activities.Statements.Confirm> 活动为 <xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> 中包含的活动显式调用 <xref:System.Activities.Statements.CompensableActivity>。 如果 <xref:System.Activities.Statements.Confirm> 活动未在 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> 的 <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>、<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> 或 <xref:System.Activities.Statements.CompensableActivity> 中使用，则必须指定 <xref:System.Activities.Statements.Confirm.Target%2A> 属性。

 由 <xref:System.Activities.Statements.CompensationToken> 指定的 <xref:System.Activities.Statements.Compensate.Target%2A> 提供了在 <xref:System.Activities.Statements.CompensableActivity> 的 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 成功完成之后显式确认或补偿 <xref:System.Activities.Statements.CompensableActivity> 的方法。

### <a name="using-the-confirm-activity-designer"></a>使用 Confirm 活动设计器
 可以在 **"** 工具箱"的"事务"类别中找到"确认"活动设计器，单击"工具箱"左侧的"工具箱"工作流设计器。  或者，从"视图 **"菜单中** 选择"**工具箱"，** 或按 **Ctrl** + **Alt** + **X**。

 "**确认**"活动设计器可以从"工具箱"拖动到工作流设计器放置活动（例如位于 内）的"确认"图面 <xref:System.Activities.Statements.Sequence> 。 这将创建具有 Confirm 的默认 <xref:System.Activities.Statements.Confirm> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 可以在 Confirm 活动设计器的标头或属性网格的 <xref:System.Activities.Activity.DisplayName%2A> **DisplayName** 框中编辑该值。 

### <a name="the-confirm-properties"></a>Confirm 属性
 下表列出 <xref:System.Activities.Statements.Confirm> 属性并说明如何在设计器中使用它们。 可以在属性网格中或在工作流设计器编辑属性，但必须在属性网格 <xref:System.Activities.Activity.DisplayName%2A> <xref:System.Activities.Statements.Confirm.Target%2A> 中编辑该属性。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.CancellationScope> 活动的可选友好名称。 默认值为 Confirm。|
|<xref:System.Activities.Statements.Confirm.Target%2A>|正确|指定 <xref:System.Activities.InArgument%601>，它包含此 <xref:System.Activities.Statements.CompensationToken> 活动的 <xref:System.Activities.Statements.Confirm>。|

## <a name="see-also"></a>请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)