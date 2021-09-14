---
title: CompensableActivity 活动设计器
description: 了解如何在工作流设计器中使用 "CompensableActivity" 活动设计器来创建和配置 CompensableActivity 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CompensableActivity.UI
ms.assetid: e0340d89-d39e-4a52-8557-13e27040d7b5
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: b3334b2be145dd01bd89fcc0b0d792238e9a684f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602195"
---
# <a name="compensableactivity-activity-designer"></a>CompensableActivity 活动设计器

" **CompensableActivity** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.CompensableActivity> 活动。

## <a name="the-compensableactivity-activity"></a>CompensableActivity 活动
 <xref:System.Activities.Statements.CompensableActivity> 定义可在成功完成之后得到确认或补偿的工作单元。

### <a name="using-the-compensableactivity-activity-designer"></a>使用 CompensableActivity 活动设计器
 " **CompensableActivity** " 活动设计器可在 "**工具箱**" 的 "**事务**" 类别中找到。 若要打开 **工具箱**，请选择工作流设计器左侧的 " **工具箱** " 选项卡。 或者，从 "**视图**" 菜单中选择 **"工具箱**"，或按 **Ctrl** + **Alt** + **X**。

 可以将 " **CompensableActivity** " 活动设计器从 **"工具箱** " 拖放到工作流设计器图面上。 您可以将活动设计器放在中 <xref:System.Activities.Statements.Sequence> 。 删除活动设计器将创建一个 <xref:System.Activities.Statements.CompensableActivity> 活动，其默认值为 <xref:System.Activities.Activity.DisplayName%2A> CompensableActivity。 编辑 " <xref:System.Activities.Activity.DisplayName%2A> **CompensableActivity** " 活动设计器的标头中的值。 它还可在属性网格的 " **DisplayName** " 框中进行编辑。

### <a name="the-compensableactivity-properties"></a>CompensableActivity 属性
 下表列出 <xref:System.Activities.Statements.CompensableActivity> 属性并说明如何在设计器中使用它们。 <xref:System.Activities.Activity.DisplayName%2A>和 <xref:System.Activities.Activity%601.Result%2A> 属性可在属性网格中进行编辑，但其他属性必须在工作流设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.CompensableActivity> 活动的可选友好名称。 默认值为 CompensableActivity。|
|<xref:System.Activities.Activity%601.Result%2A>|错误|指定 <xref:System.Activities.Statements.CompensableActivity> 的返回值。 此属性必须在属性网格中进行编辑。|
|<xref:System.Activities.Statements.CompensableActivity.Body%2A>|正确|指定为其提供补偿、取消和确认逻辑的活动。 若要添加 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动，请将 **"工具箱**" 中的活动拖放到 " **CompensableActivity** " 活动设计器的 "**正文**" 框中。 添加提示文本 "在此处放置活动"。|
|<xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>|错误|指定在取消时执行的活动。 若要添加活动，请将其设计器从 **"工具箱**" 拖到 " **CompensableActivity** " 活动设计器上的 " **CancellationHandler** " 框。 添加提示文本 "在此处放置活动"。|
|<xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>|错误|指定补偿 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动时要执行的活动。 可使用 <xref:System.Activities.Statements.Compensate> 活动显式调用此处理程序。<br /><br /> 若要添加活动，请将其活动设计器从 **"工具箱**" 拖到 " **CompensableActivity** " 活动设计器上的 " **CompensationHandler** " 框中。 添加提示文本 "在此处放置活动"。|
|<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>|错误|指定确认 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动时要执行的活动。 可使用 <xref:System.Activities.Statements.Confirm> 活动显式调用此处理程序。<br /><br /> 若要添加活动，请将其活动设计器从 **"工具箱**" 拖到 " **CompensableActivity** " 活动设计器上的 " **ConfirmationHandler** " 框中。 添加提示文本 "在此处放置活动"。|

## <a name="see-also"></a>另请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [确认](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)
