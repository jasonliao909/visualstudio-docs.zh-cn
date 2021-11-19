---
title: SendAndReceiveReply 模板设计器
description: 了解如何使用工作流设计器中的 SendAndReceiveReply 模板来创建一对预配置的 Send 和 ReceiveReply 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.SendAndReceiveReply.UI
- System.ServiceModel.Activities.ReceiveReply.UI
ms.assetid: 818a8c84-6593-416d-b016-1d91b85ffb68
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 6a6a91c562750898fd085f1b32d8c299a8604d93
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666971"
---
# <a name="sendandreceivereply-template-designer"></a>SendAndReceiveReply 模板设计器

SendAndReceiveReply 模板用于创建一对预配置的 <xref:System.ServiceModel.Activities.Send> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 活动。 这些活动是 <xref:System.Activities.Statements.Sequence> 活动的一部分，并作为客户端上请求/响应消息交换模式的一部分相互关联。

## <a name="the-sendandreceivereply-template"></a>SendAndReceiveReply 模板

除了在 <xref:System.Activities.Statements.Sequence> 活动中创建 <xref:System.ServiceModel.Activities.Send> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 活动之外，添加 SendAndReceiveReply 模板还要完成三个任务：

- 配置 <xref:System.ServiceModel.Activities.Send> 活动的 <xref:System.ServiceModel.Activities.Send.OperationName%2A> 和 <xref:System.ServiceModel.Activities.Send.ServiceContractName%2A> 属性。

- 将 <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> 活动的 <xref:System.ServiceModel.Activities.ReceiveReply> 属性绑定到 <xref:System.ServiceModel.Activities.Send> 活动。

- 创建一个 <xref:System.ServiceModel.Activities.CorrelationHandle> 作为父活动中的一个变量。

### <a name="use-the-sendandreceivereply-template-designer"></a>使用 SendAndReceiveReply 模板设计器

访问“工具箱”的“消息”类别中的 SendAndReceiveReply 活动设计器  。 可以将 SendAndReceiveReply 活动设计器从“工具箱”拖放到工作流设计器图面上通常放置活动的任何位置 。 拖放活动设计器将创建一个可以使用 Send 活动设计器配置的 <xref:System.ServiceModel.Activities.Send> 活动，以及一个可以使用 ReceiveReplyForSend 设计器配置的相关 <xref:System.ServiceModel.Activities.ReceiveReply> 。

有关使用 Send 设计器配置 <xref:System.ServiceModel.Activities.Send> 活动的更多信息，请参见 [Send](../workflow-designer/send-activity-designer.md) 主题。

### <a name="properties-of-receivereply"></a>ReceiveReply 的属性

下表显示 <xref:System.ServiceModel.Activities.ReceiveReply> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在工作流设计器图面上进行编辑。

| 属性名称 | 必选 | 使用情况 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | 错误 | <xref:System.ServiceModel.Activities.ReceiveReply> 活动的可选友好名称。 默认值为 ReceiveReplyForSend。<br /><br /> 虽然对友好 <xref:System.Activities.Activity.DisplayName%2A> 使用非默认值不是绝对必需的，但最好使用非默认值。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> | True | 对与此 <xref:System.ServiceModel.Activities.Send> 活动配对的 <xref:System.ServiceModel.Activities.ReceiveReply> 活动的引用。 此属性不得为 NULL。 在客户端上将 <xref:System.ServiceModel.Activities.Send> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 活动配合使用，可对请求/响应消息模式建模。 此属性指定配对的 <xref:System.ServiceModel.Activities.Send> 活动。 在该设计器中无法编辑此属性，因为它自动绑定到从中创建了 <xref:System.ServiceModel.Activities.ReceiveReply> 活动的 <xref:System.ServiceModel.Activities.Send> 活动。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.Content%2A> | 错误 | 指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 编辑此属性的方法是单击属性网格中“内容”字段旁的省略号按钮，或单击 Receive 活动设计器图面上“内容”标签旁的“定义”按钮   。 两者都显示“内容定义”对话框。 有关如何使用此对话框的详细信息，请参阅[“内容定义”对话框](../workflow-designer/content-definition-dialog-box.md)。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.CorrelationInitializers%2A> | 错误 | 指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Receive> 对象的集合。 在属性网格中单击 <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> 属性旁边的省略号按钮，以打开“添加相关初始值设定项”对话框。 有关使用此框的详细信息，请参阅[“添加相关初始值设定项”对话框](../workflow-designer/add-correlationinitializers-dialog-box.md)。 |
| <xref:System.ServiceModel.Activities.ReceiveReply.Action%2A> | 错误 | 指定消息的操作标头。 如果未显式设置，则它的值默认为：<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}`. |

## <a name="see-also"></a>另请参阅

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [Receive](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- 发送
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)