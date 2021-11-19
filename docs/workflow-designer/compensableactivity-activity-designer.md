---
title: CompensableActivity 活动设计器
description: 了解如何在工作流设计器中使用 CompensableActivity 活动设计器来创建和配置 CompensableActivity 活动。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602195"
---
# <a name="compensableactivity-activity-designer"></a>CompensableActivity 活动设计器

CompensableActivity 活动设计器用于创建和配置 <xref:System.Activities.Statements.CompensableActivity> 活动。

## <a name="the-compensableactivity-activity"></a>CompensableActivity 活动
 <xref:System.Activities.Statements.CompensableActivity> 定义可在成功完成之后得到确认或补偿的工作单元。

### <a name="using-the-compensableactivity-activity-designer"></a>使用 CompensableActivity 活动设计器
 可在“工具箱”的“事务”类别中找到 CompensableActivity 活动设计器。 若要打开“工具箱”，请选择工作流设计器左侧的“工具箱”选项卡。 或者，从“视图”菜单栏中选择“工具箱”或按 Ctrl+Alt+X。

 可以将 CompensableActivity 活动设计器从“工具箱”拖放到工作流设计器图面上。 可以将活动设计器拖放到 <xref:System.Activities.Statements.Sequence> 中。 放置活动设计器将创建一个 <xref:System.Activities.Statements.CompensableActivity> 活动，其默认 <xref:System.Activities.Activity.DisplayName%2A> 为 CompensableActivity。 编辑 CompensableActivity 活动设计器标头中的 <xref:System.Activities.Activity.DisplayName%2A> 值。 还可以在属性网格的“DisplayName”框中编辑它。

### <a name="the-compensableactivity-properties"></a>CompensableActivity 属性
 下表列出 <xref:System.Activities.Statements.CompensableActivity> 属性并说明如何在设计器中使用它们。 <xref:System.Activities.Activity.DisplayName%2A> 和 <xref:System.Activities.Activity%601.Result%2A> 属性可在属性网格中编辑，但其他属性必须在工作流设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.CompensableActivity> 活动的可选友好名称。 默认值为 CompensableActivity。|
|<xref:System.Activities.Activity%601.Result%2A>|错误|指定 <xref:System.Activities.Statements.CompensableActivity> 的返回值。 此属性必须在属性网格中进行编辑。|
|<xref:System.Activities.Statements.CompensableActivity.Body%2A>|True|指定为其提供补偿、取消和确认逻辑的活动。 若要添加 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动，请将活动从“工具箱”拖到 CompensableActivity 活动设计器上的“正文”框中。 添加提示文本“在此处放置活动”。|
|<xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>|错误|指定在取消时执行的活动。 若要添加活动，请将该活动的设计器从“工具箱”拖放到 CompensableActivity 活动设计器”的“CancellationHandler”框中。 添加提示文本“在此处放置活动”。|
|<xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>|错误|指定补偿 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动时要执行的活动。 可使用 <xref:System.Activities.Statements.Compensate> 活动显式调用此处理程序。<br /><br /> 若要添加活动，请将其活动设计器从“工具箱”拖放到 CompensableActivity 活动设计器”的“CompensationHandler”框中。 添加提示文本“在此处放置活动”。|
|<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>|错误|指定确认 <xref:System.Activities.Statements.CompensableActivity.Body%2A> 活动时要执行的活动。 可使用 <xref:System.Activities.Statements.Confirm> 活动显式调用此处理程序。<br /><br /> 若要添加活动，请将其活动设计器从“工具箱”拖放到 CompensableActivity 活动设计器”的“ConfirmationHandler”框中。 添加提示文本“在此处放置活动”。|

## <a name="see-also"></a>另请参阅

- [事务](../workflow-designer/transaction-activity-designers.md)
- [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [确认](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)
