---
title: 工作流设计器 CorrelationScope 活动设计器
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122135359"
---
# <a name="correlationscope-activity-designer"></a>CorrelationScope 活动设计器

" **CorrelationScope** " 活动设计器用于创建和配置 <xref:System.ServiceModel.Activities.CorrelationScope> 活动，该活动使用对象提供子消息传递活动的隐式管理 <xref:System.ServiceModel.Activities.CorrelationHandle> 。

## <a name="the-correlationscope-activity"></a>CorrelationScope 活动

<xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> 属性指定用于管理子消息传递活动的 <xref:System.ServiceModel.Activities.CorrelationHandle>。 将 <xref:System.ServiceModel.Activities.Send> 中包含的 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.CorrelationScope.Body%2A> 活动配置为使用包含 <xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> 活动的 <xref:System.ServiceModel.Activities.CorrelationScope> 属性以执行相关。

### <a name="use-the-correlationscope-activity-designer"></a>使用 CorrelationScope 活动设计器

" **CorrelationScope** " 活动设计器可在 "**工具箱**" 的 "**消息传送**" 类别中找到，可通过单击工作流设计器左侧的 "**工具箱**" 选项卡进行访问。 或者，从 "**视图**" 菜单中选择 **"工具箱**"，或按 **Ctrl** + **Alt** + **X**。

可以将 " **CorrelationScope** " 活动设计器从 " **工具箱** " 拖放到工作流设计器图面上。 这将创建 <xref:System.ServiceModel.Activities.CorrelationScope> 具有 CorrelationScope 的默认 **DisplayName** 的活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在 " **CorrelationScope** " 活动设计器的标头中或在 "**属性**" 窗口的 " **DisplayName** " 框中编辑。

若要指定 <xref:System.ServiceModel.Activities.CorrelationHandle> 子消息传递活动使用的，请在 "**属性**" 窗口中选择 " **CorrelatesWith** " 字段旁边的省略号按钮，以显示 "**表达式编辑器**" 对话框。 还可以在活动设计器图面上设置此属性。

在相关范围内的活动是通过在 **CorrelationScope** 设计器内的 "**正文**" 框中删除其设计器来指定的。

### <a name="the-correlationscope-properties"></a>CorrelationScope 属性

下表列出 <xref:System.ServiceModel.Activities.CorrelationScope> 属性并说明如何在设计器中使用它们。 这些属性可以在 " **属性** " 窗口中或在工作流设计器图面上进行编辑，也可以在这两种情况下编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.ServiceModel.Activities.InitializeCorrelation> 活动的可选友好名称。|
|<xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A>|错误|指定用于管理子消息传递活动的 <xref:System.ServiceModel.Activities.CorrelationHandle>。 如果未设置此属性，则 <xref:System.ServiceModel.Activities.CorrelationScope> 会自动创建一个隐式 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|<xref:System.ServiceModel.Activities.CorrelationScope.Body%2A>|错误|指定处于相关范围之内的活动。|

## <a name="see-also"></a>请参阅

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [收](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- 发送
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)