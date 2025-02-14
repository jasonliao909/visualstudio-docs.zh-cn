---
title: 工作流设计器 - CorrelationScope 活动设计器
description: 了解如何使用 CorrelationScope 活动设计器创建和配置 CorrelationScope 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.CorrelationScope.UI
ms.assetid: 75f20664-9042-464d-8e2b-148d365a2286
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: d496ca8f3d578a3cac15374f0c79629b39b6b0f8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666113"
---
# <a name="correlationscope-activity-designer"></a>CorrelationScope 活动设计器

“CorrelationScope”活动设计器用于创建和配置 <xref:System.ServiceModel.Activities.CorrelationScope> 活动，该活动使用 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象提供子消息传递活动的隐式管理。

## <a name="the-correlationscope-activity"></a>CorrelationScope 活动

<xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> 属性指定用于管理子消息传递活动的 <xref:System.ServiceModel.Activities.CorrelationHandle>。 将 <xref:System.ServiceModel.Activities.Send> 中包含的 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.CorrelationScope.Body%2A> 活动配置为使用包含 <xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> 活动的 <xref:System.ServiceModel.Activities.CorrelationScope> 属性以执行相关。

### <a name="use-the-correlationscope-activity-designer"></a>使用 CorrelationScope 活动设计器

可以在“工具箱”的“消息”类别中找到“CorrelationScope”活动设计器，通过单击工作流设计器左侧的“工具箱”选项卡来访问   。 或者，从“视图”菜单栏中选择“工具箱”或按 Ctrl+Alt+X    。

可以将“CorrelationScope”活动设计器从“工具箱”拖放到工作流设计器图面上 。 这将创建具有 CorrelationScope 的默认“DisplayName”的 <xref:System.ServiceModel.Activities.CorrelationScope> 活动。 可以在“CorrelationScope”活动设计器的标头中或在“属性”窗口的“DisplayName”框中编辑 <xref:System.Activities.Activity.DisplayName%2A>  。

若要指定子消息传递活动所使用的 <xref:System.ServiceModel.Activities.CorrelationHandle>，请选择“属性”窗口中“CorrelatesWith”字段旁的椭圆形按钮以显示“表达式编辑器”对话框  。 还可以在活动设计器图面上设置此属性。

通过将活动设计器放置在“CorrelationScope”设计器的“Body”框中可指定范围在相关之内的活动 。

### <a name="the-correlationscope-properties"></a>CorrelationScope 属性

下表列出 <xref:System.ServiceModel.Activities.CorrelationScope> 属性并说明如何在设计器中使用它们。 这些属性可以在“属性”窗口中编辑，也可以在工作流设计器图面上编辑，通常在这两者中都可以进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.ServiceModel.Activities.InitializeCorrelation> 活动的可选友好名称。|
|<xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A>|错误|指定用于管理子消息传递活动的 <xref:System.ServiceModel.Activities.CorrelationHandle>。 如果未设置此属性，则 <xref:System.ServiceModel.Activities.CorrelationScope> 会自动创建一个隐式 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|<xref:System.ServiceModel.Activities.CorrelationScope.Body%2A>|错误|指定处于相关范围之内的活动。|

## <a name="see-also"></a>另请参阅

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [Receive](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- 发送
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)