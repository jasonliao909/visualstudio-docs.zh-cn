---
title: TransactedReceiveScope 活动设计器
description: 在工作流设计器中，了解如何使用 TransactedReceiveScope 设计器创建和配置 TransactedReceiveScope 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.TransactedReceiveScope.UI
ms.assetid: 7ca93aad-4e83-4d81-90f4-998ee114d9b6
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: cbdbd2ce46e5d9d6bf9f0f69c81c9bfdaa0b1d6d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666102"
---
# <a name="transactedreceivescope-activity-designer"></a>TransactedReceiveScope 活动设计器

TransactedReceiveScope 设计器用于创建和配置 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 活动。

## <a name="the-transactedreceivescope-activity"></a>TransactedReceiveScope 活动

<xref:System.ServiceModel.Activities.TransactedReceiveScope> 活动使你能够将事务流动到工作流或调度程序创建的服务器事务中。

### <a name="using-the-transactedreceivescope-activity-designer"></a>使用 TransactedReceiveScope 活动设计器

访问“工具箱”的“消息”类别中的 TransactedReceiveScope 活动设计器  。 可以将 TransactedReceiveScope 活动设计器从“工具箱”拖放到工作流设计器图面上通常放置活动的任何位置 。 这将创建具有 TransactedReceiveScope 的默认“DisplayName”的 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 活动。 可以在 TransactedReceiveScope 活动设计器的标头中或在属性网格的“DisplayName”框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 。

TransactedReceiveScope 设计器包含“Request”和“Body”框  。 它们用于配置 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A> 属性，该属性指定一个 <xref:System.ServiceModel.Activities.Receive> 活动和一个指定某些其他 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A> 的 <xref:System.Activities.Activity> 属性。 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A> 创建一个事务。 然后使该事务成为 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A> 范围的环境事务以便此范围中的任何活动可在该事务内执行。

### <a name="the-transactedreceivescope-properties"></a>TransactedReceiveScope 属性

下表列出 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 属性并说明如何在设计器中使用它们。 这些 <xref:System.Activities.Activity.DisplayName%2A> 属性可在属性网格中或工作流设计器图面上进行编辑，但其他属性必须在设计图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.ServiceModel.Activities.TransactedReceiveScope> 活动的可选友好名称。 默认值为 TransactedReceiveScope。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 名称不是绝对必需的，但最好使用显示名称。|
|<xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A>|True|将 <xref:System.ServiceModel.Activities.Receive> 活动放置在活动设计器图面上的“Request”块中。|
|<xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A>|错误|将 <xref:System.Activities.Activity> 活动放置在活动设计器图面上的“Body”块中。|

## <a name="see-also"></a>另请参阅

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [Receive](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- 发送
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)