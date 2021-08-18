---
title: TransactedReceiveScope 活动设计器
description: 在工作流设计器，了解如何使用 TransactedReceiveScope 设计器创建和配置 TransactedReceiveScope 活动。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122135112"
---
# <a name="transactedreceivescope-activity-designer"></a>TransactedReceiveScope 活动设计器

**TransactedReceiveScope** 设计器用于创建和配置 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 活动。

## <a name="the-transactedreceivescope-activity"></a>TransactedReceiveScope 活动

<xref:System.ServiceModel.Activities.TransactedReceiveScope> 活动使你能够将事务流动到工作流或调度程序创建的服务器事务中。

### <a name="using-the-transactedreceivescope-activity-designer"></a>使用 TransactedReceiveScope 活动设计器

访问"工具箱"的"消息传送"类别中的 **TransactedReceiveScope** 活动 **设计器**。 **TransactedReceiveScope** 活动设计器可以从工具箱拖动，并拖放到工作流设计器放置活动的位置。 这会创建默认 <xref:System.ServiceModel.Activities.TransactedReceiveScope> **DisplayName** 为 TransactedReceiveScope 的活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在 **TransactedReceiveScope** 活动设计器的标头或属性网格的 **DisplayName** 框中编辑 。

**TransactedReceiveScope** 设计器包含 **"请求"和"****正文"** 框。 它们用于配置 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A> 属性，该属性指定一个 <xref:System.ServiceModel.Activities.Receive> 活动和一个指定某些其他 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A> 的 <xref:System.Activities.Activity> 属性。 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A> 创建一个事务。 然后使该事务成为 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A> 范围的环境事务以便此范围中的任何活动可在该事务内执行。

### <a name="the-transactedreceivescope-properties"></a>TransactedReceiveScope 属性

下表列出 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 属性并说明如何在设计器中使用它们。 可以在属性网格或工作流设计器编辑该属性，但必须在设计图面上编辑 <xref:System.Activities.Activity.DisplayName%2A> 其他属性。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.ServiceModel.Activities.TransactedReceiveScope> 活动的可选友好名称。 默认值为 TransactedReceiveScope。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 名称不是绝对必需的，但最好使用显示名称。|
|<xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A>|正确|将 <xref:System.ServiceModel.Activities.Receive> 活动放入活动设计器 **图** 面上的 Request 块。|
|<xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A>|错误|将 <xref:System.Activities.Activity> 放入活动 **设计器图** 面上的 Body 块。|

## <a name="see-also"></a>请参阅

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [收到](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- 发送
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)