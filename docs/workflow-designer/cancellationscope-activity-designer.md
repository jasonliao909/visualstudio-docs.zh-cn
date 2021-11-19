---
title: CancellationScope 活动设计器
description: 了解如何使用中的 CancellationScope 活动设计器工作流设计器和配置 CancellationScope 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CancellationScope.UI
ms.assetid: 2c85d663-b219-4142-9866-7693ffd46379
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 91eb31444a56d68f062f7909d9fb5de13d3f496d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602198"
---
# <a name="cancellationscope-activity-designer"></a>CancellationScope 活动设计器

**CancellationScope** 活动设计器用于创建和配置 <xref:System.Activities.Statements.CancellationScope> 活动。

## <a name="the-cancellationscope-activity"></a>CancellationScope 活动

使用 <xref:System.Activities.Statements.CancellationScope> 活动可指定要执行的活动以及该活动的取消逻辑。

### <a name="using-the-cancellationscope-activity-designer"></a>使用 CancellationScope 活动设计器

**CancellationScope** 活动设计器可以在"工具箱"的 **"事务"****类别中找到**。 若要打开 **"工具箱**"， **请选择"** 工具箱"选项卡工作流设计器。 或者，从"视图 **"菜单中** 选择"**工具箱"，** 或按 **Ctrl** + **Alt** + **X**。

**CancellationScope** 活动设计器可以从"工具箱"拖动到工作流设计器放置活动（例如位于 内）的图面上 <xref:System.Activities.Statements.Sequence> 。 删除 **CancellationScope** 活动设计器会创建 <xref:System.Activities.Statements.CancellationScope> 一个默认为 <xref:System.Activities.Activity.DisplayName%2A> CancellationScope 的活动。 编辑 <xref:System.Activities.Activity.DisplayName%2A> **CancellationScope** 活动设计器标头中的值。 还可以在属性网格的 **"DisplayName"** 框中编辑它。

### <a name="the-cancellationscope-properties"></a>CancellationScope 属性

下表列出 <xref:System.Activities.Statements.CancellationScope> 属性并说明如何在设计器中使用它们。 <xref:System.Activities.Activity.DisplayName%2A>属性可以在属性网格中编辑，但其他属性必须在工作流设计器编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.CancellationScope> 活动的可选友好名称。 默认值为 CancellationScope。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.CancellationScope.Body%2A>|True|指定为其提供取消逻辑的活动。 若要添加活动，请从"工具箱"将活动拖放到 CancellationScope 活动设计器上的 <xref:System.Activities.Statements.CancellationScope.Body%2A> **"正文**"框中。   添加提示文本"此处放置活动"。|
|<xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>|True|指定在取消时执行的活动。 若要添加活动，请从"工具箱"将活动拖放到 CancellationScope 活动设计器上的 <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> **CancellationHandler** 框中。  添加提示文本"此处放置活动"。|

## <a name="see-also"></a>另请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [确认](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)
