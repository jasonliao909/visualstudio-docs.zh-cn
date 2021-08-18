---
title: ReceiveAndSendReply 模板设计器
description: 了解如何使用 工作流设计器 中的 ReceiveAndSendReply 模板创建一对预配置的 Receive 和 SendReply 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.ReceiveAndSendReply.UI
- System.ServiceModel.Activities.SendReply.UI
ms.assetid: d1d9a058-df7e-48f5-a2e7-3caeeba7eaa6
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: ba89478dcbc69104c89788708afe32e338ef7071
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122135294"
---
# <a name="receiveandsendreply-template-designer"></a>ReceiveAndSendReply 模板设计器

**ReceiveAndSendReply** 模板用于创建一对预配置的 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动。 活动是活动的一部分，并作为服务器上请求/响应消息 <xref:System.Activities.Statements.Sequence> 交换模式的一部分相关联。

## <a name="the-receiveandsendreply-template"></a>ReceiveAndSendReply 模板

添加 **ReceiveAndSendReply** 模板除了使用 活动创建 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动外，还执行三 <xref:System.Activities.Statements.Sequence> 项操作：

- 配置活动的 <xref:System.ServiceModel.Activities.Receive.OperationName%2A> <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> 和 <xref:System.ServiceModel.Activities.Receive> 属性。

- 将 <xref:System.ServiceModel.Activities.SendReply.Request%2A> 活动的 <xref:System.ServiceModel.Activities.Receive> 属性绑定到 <xref:System.ServiceModel.Activities.Send> 活动。

- 创建一个 <xref:System.ServiceModel.Activities.CorrelationHandle> 作为父活动中的一个变量。

### <a name="use-the-receiveandsendreply-template-designer"></a>使用 ReceiveAndSendReply 模板设计器

访问"工具箱"的"消息"类别中 **的** **ReceiveAndSendReply** 活动 **设计器**。 **ReceiveAndSendReply** 活动设计器可以从工具箱拖动，并拖放到工作流设计器放置活动的位置。 删除活动设计器会创建一个活动，该活动可以使用 Send 活动设计器进行配置，并创建一个可以使用 <xref:System.ServiceModel.Activities.Receive>  <xref:System.ServiceModel.Activities.SendReply> SendReplyToReceive 设计器配置的关联活动。

有关使用接收设计器配置活动的信息， <xref:System.ServiceModel.Activities.Receive> 请参阅[接收活动设计器](../workflow-designer/receive-activity-designer.md)。

### <a name="properties-of-sendreply"></a>SendReply 的属性

下表列出 <xref:System.ServiceModel.Activities.SendReply> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中编辑，某些属性可以在工作流设计器编辑。

| 属性名称 | 必选 | 使用情况 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | 错误 | <xref:System.ServiceModel.Activities.SendReply> 活动的可选友好名称。 默认值为 SendReplyToReceive。<br /><br /> 虽然不严格要求对友好项使用非默认值，但 <xref:System.Activities.Activity.DisplayName%2A> 最好使用此类值。 |
| <xref:System.ServiceModel.Activities.SendReply.Request%2A> | 正确 | 对与此 <xref:System.ServiceModel.Activities.Receive> 活动配对的 <xref:System.ServiceModel.Activities.SendReply> 活动的引用。 此属性不能为 **null**。 <xref:System.ServiceModel.Activities.Receive><xref:System.ServiceModel.Activities.SendReply>和 活动在服务器上一起用于为请求/响应消息传送模式建模。 此属性指定配对的 <xref:System.ServiceModel.Activities.Send> 活动。 在设计器中，无法编辑此属性，因为它会自动绑定到 <xref:System.ServiceModel.Activities.Send> 从中创建活动 <xref:System.ServiceModel.Activities.SendReply> 的活动。 |
| <xref:System.ServiceModel.Activities.SendReply.Content%2A> | 错误 | 指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 通过单击属性网格中"内容"字段旁边的省略号按钮，或单击"接收活动设计器"图面上"内容"标签旁边的"定义"按钮来编辑此属性。  两者都显示 **"内容定义"** 对话框。 有关如何使用此框的详细信息，请参阅内容 [定义对话框](../workflow-designer/content-definition-dialog-box.md) 主题。 |
| <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> | 错误 | 指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Receive> 对象的集合。 单击属性网格中属性旁边的省略号 <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> 按钮，打开" **添加相关初始值设置项** "对话框。 有关使用此框的详细信息，请参阅添加 [CorrelationInitializers 对话框](../workflow-designer/add-correlationinitializers-dialog-box.md) 主题。 |
| <xref:System.ServiceModel.Activities.SendReply.Action%2A> | 错误 | 指定消息的操作标头。 如果未显式设置，则其值默认为：<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}` |
| <xref:System.ServiceModel.Activities.SendReply.PersistBeforeSend%2A> | 错误 | 指定在发送回复消息前是否应保留工作流实例。 默认值是 **false** 秒。 |

## <a name="see-also"></a>请参阅

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [收到](../workflow-designer/receive-activity-designer.md)
- 发送
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)