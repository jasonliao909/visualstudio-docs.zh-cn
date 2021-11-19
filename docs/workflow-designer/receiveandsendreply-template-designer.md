---
title: ReceiveAndSendReply 模板设计器
description: 了解如何使用工作流设计器中的 ReceiveAndSendReply 模板创建一对预配置的 Receive 和 SendReply 活动。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664673"
---
# <a name="receiveandsendreply-template-designer"></a>ReceiveAndSendReply 模板设计器

ReceiveAndSendReply 模板用于创建一对预配置的 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动。 这些活动是 <xref:System.Activities.Statements.Sequence> 活动的一部分，并作为服务器上请求/响应消息交换模式的一部分相互关联。

## <a name="the-receiveandsendreply-template"></a>ReceiveAndSendReply 模板

添加“ReceiveAndSendReply”模板除了在 <xref:System.Activities.Statements.Sequence> 活动中创建 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动之外，还要完成三个任务：

- 配置 <xref:System.ServiceModel.Activities.Receive> 活动的 <xref:System.ServiceModel.Activities.Receive.OperationName%2A> 和 <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> 属性。

- 将 <xref:System.ServiceModel.Activities.SendReply.Request%2A> 活动的 <xref:System.ServiceModel.Activities.Receive> 属性绑定到 <xref:System.ServiceModel.Activities.Send> 活动。

- 创建一个 <xref:System.ServiceModel.Activities.CorrelationHandle> 作为父活动中的一个变量。

### <a name="use-the-receiveandsendreply-template-designer"></a>使用 ReceiveAndSendReply 模板设计器

访问“工具箱”的“消息”类别中的 ReceiveAndSendReply 活动设计器。 可以将 ReceiveAndSendReply 活动设计器从“工具箱”拖放到工作流设计器图面上通常放置活动的任何位置。 拖放活动设计器将创建一个可以使用 Send 活动设计器配置的 <xref:System.ServiceModel.Activities.Receive> 活动，以及一个可以使用 SendReplyToReceive 设计器配置的相关 <xref:System.ServiceModel.Activities.SendReply>。

有关使用 Receive 设计器配置 <xref:System.ServiceModel.Activities.Receive> 活动的更多信息，请参见 [Receive 活动设计器](../workflow-designer/receive-activity-designer.md)。

### <a name="properties-of-sendreply"></a>SendReply 的属性

下表列出 <xref:System.ServiceModel.Activities.SendReply> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在工作流设计器图面上进行编辑。

| 属性名称 | 必选 | 使用情况 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | 错误 | <xref:System.ServiceModel.Activities.SendReply> 活动的可选友好名称。 默认值为 SendReplyToReceive。<br /><br /> 虽然对友好 <xref:System.Activities.Activity.DisplayName%2A> 使用非默认值不是绝对必需的，但最好使用非默认值。 |
| <xref:System.ServiceModel.Activities.SendReply.Request%2A> | True | 对与此 <xref:System.ServiceModel.Activities.Receive> 活动配对的 <xref:System.ServiceModel.Activities.SendReply> 活动的引用。 此属性不得为 NULL。 在服务器上将 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动配合使用，可对请求/响应消息模式进行建模。 此属性指定配对的 <xref:System.ServiceModel.Activities.Send> 活动。 在该设计器中无法编辑此属性，因为它自动绑定到从中创建了 <xref:System.ServiceModel.Activities.SendReply> 活动的 <xref:System.ServiceModel.Activities.Send> 活动。 |
| <xref:System.ServiceModel.Activities.SendReply.Content%2A> | 错误 | 指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 编辑此属性的方法是单击属性网格中“内容”字段旁的省略号按钮，或单击 Receive 活动设计器图面上“内容”标签旁的“定义”按钮。 这两者都会显示“内容定义”对话框。 若要详细了解如何使用此框，请参阅[“内容定义”对话框](../workflow-designer/content-definition-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> | 错误 | 指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Receive> 对象的集合。 在属性网格中单击 <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> 属性旁边的省略号按钮，打开“添加相关初始值设定项”对话框。 若要详细了解如何使用此框，请参阅[“添加相关初始值设定项”对话框](../workflow-designer/add-correlationinitializers-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.SendReply.Action%2A> | 错误 | 指定消息的操作标头。 如果未显式设置，则它的值默认为：<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}` |
| <xref:System.ServiceModel.Activities.SendReply.PersistBeforeSend%2A> | 错误 | 指定在发送回复消息前是否应保留工作流实例。 默认值是 **false** 秒。 |

## <a name="see-also"></a>另请参阅

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [Receive](../workflow-designer/receive-activity-designer.md)
- 发送
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)