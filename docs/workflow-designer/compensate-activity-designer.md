---
title: 工作流设计器 - 补偿活动设计器
description: 了解"补偿"活动设计器，以及如何使用"补偿"活动设计器创建和配置"补偿"活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Compensate.UI
ms.assetid: 7347c947-bfff-4bad-becd-5cd23e7b24cd
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: ca9c66d68913e0791daea6736c7bb5aeeead4df2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122068098"
---
# <a name="compensate-activity-designer"></a>Compensate 活动设计器

**Compensate** 活动设计器用于创建和配置 <xref:System.Activities.Statements.Compensate> 活动。

## <a name="the-compensate-activity"></a>Compensate 活动

<xref:System.Activities.Statements.Compensate> 活动为 <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> 中包含的活动显式调用 <xref:System.Activities.Statements.CompensableActivity>。 如果 <xref:System.Activities.Statements.Compensate> 活动未在 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> 的 <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>、<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> 或 <xref:System.Activities.Statements.CompensableActivity> 中使用，则必须指定 <xref:System.Activities.Statements.Compensate.Target%2A> 属性。

由 <xref:System.Activities.Statements.CompensationToken> 指定的 <xref:System.Activities.Statements.Compensate.Target%2A> 提供了在 <xref:System.Activities.Statements.CompensableActivity> 的 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 成功完成之后显式确认或补偿 <xref:System.Activities.Statements.CompensableActivity> 的方法。

### <a name="using-the-compensate-activity-designer"></a>使用 Compensate 活动设计器

可以在"工具箱"的"事务 **"** 类别中找到 **"补偿**"**活动设计器**。 若要打开 **"工具箱**"，请选择"工具箱"选项卡工作流设计器。 或者，从"视图 **"菜单中** 选择"**工具箱"，** 或按 **Ctrl** + **Alt** + **X**。

可 **拖动"** 补偿"活动设计器，将其从"工具箱"拖放到工作流设计器放置活动的位置（例如 位于 内）的图面上 <xref:System.Activities.Statements.Sequence> 。 删除活动设计器会创建 <xref:System.Activities.Statements.Compensate> 一个默认为 <xref:System.Activities.Activity.DisplayName%2A> "补偿"的活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在"补偿"活动设计器的标头或属性网格的 **"DisplayName"** 框中编辑该值。

### <a name="the-compensate-properties"></a>Compensate 属性

下表列出 <xref:System.Activities.Statements.CancellationScope> 属性并说明如何在设计器中使用它们。 可以在 <xref:System.Activities.Activity.DisplayName%2A> 属性网格中或在属性图面上编辑工作流设计器属性。 在 <xref:System.Activities.Statements.Compensate.Target%2A> 属性网格中编辑属性。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.Compensate> 活动的可选友好名称。 默认值为 Compensate。|
|<xref:System.Activities.Statements.Compensate.Target%2A>|正确|指定 <xref:System.Activities.InArgument%601>，它包含此 <xref:System.Activities.Statements.CompensationToken> 活动的 <xref:System.Activities.Statements.Compensate>。|

## <a name="see-also"></a>请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate 活动设计器](../workflow-designer/compensate-activity-designer.md)
- [确认](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)