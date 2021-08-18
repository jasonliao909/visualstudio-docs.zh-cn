---
title: 工作流设计器 - 接收活动设计器
description: 了解 Receive 活动，以及如何使用 Receive 活动设计器创建和配置 Receive 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.Receive.UI
ms.assetid: f58d3c70-944d-4bb4-90a7-e68c103caddc
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 1319dcbdbbefe6639fe6d52b4dfb5c5d5015ad22
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122045796"
---
# <a name="receive-activity-designer"></a>Receive 活动设计器

**Receive** 活动设计器用于创建和配置 <xref:System.ServiceModel.Activities.Receive> 活动。 <xref:System.ServiceModel.Activities.Receive> 活动是接收消息的活动，可接收的消息包括内置类型（如 <xref:System.ServiceModel.Channels.Message>、<xref:System.IO.Stream> 或 <xref:System.Xml.Linq.XElement>）或者应用程序定义的数据协定、消息协定或可序列化的 XML 类。

## <a name="the-receive-activity"></a>Receive 活动

<xref:System.ServiceModel.Activities.Receive> 活动可以接收一个或多个项，具体取决于所用接收内容的类型。 <xref:System.ServiceModel.Activities.SendReply> 活动可绑定到作为服务上请求/响应消息交换模式的一部分接收消息的 <xref:System.ServiceModel.Activities.Receive> 活动。

### <a name="using-the-receive-activity-designer"></a>使用 Receive 活动设计器

访问 **"工具箱** "的 **"消息传送"类别中** 的"接收" **活动设计器**。 可以 **拖动"** 接收"活动设计器，将其从"工具箱"拖放到工作流设计器放置活动的位置。 这将创建具有 Receive 的默认 <xref:System.ServiceModel.Activities.Receive> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在 Receive 活动设计器的标头或属性网格的 **DisplayName** 框中编辑 。

若要创建活动并将其绑定到所选活动，请右键单击"接收"活动设计器，单击上下文菜单中的"创建 <xref:System.ServiceModel.Activities.SendReply> <xref:System.ServiceModel.Activities.Receive> **SendReply"** 项 **，"SendReplyToReceive"** 设计器将显示在"接收"设计器下方。 <xref:System.ServiceModel.Activities.SendReply> 活动是作为服务上请求/响应消息交换模式的一部分发送答复消息的一个活动。 可以使用 **SendReplyToReceive 设计器配置** 它。

或者，"工具箱"的"消息传送"类别中的 **ReceiveAndSendReply** 模板设计器可用于创建一对预先配置的 <xref:System.ServiceModel.Activities.Receive> 和活动 <xref:System.ServiceModel.Activities.SendReply> 。 有关使用 **ReceiveAndSendReply** 和 **SendReplyToReceive** 模板的详细信息，请参阅 [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md) 主题。

### <a name="the-receive-activity-properties"></a>Receive 活动属性

下表列出 <xref:System.ServiceModel.Activities.Receive> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中编辑，也可以编辑工作流设计器图面。 唯一必需的属性是 <xref:System.ServiceModel.Activities.Receive.OperationName%2A> 属性。

| 属性名称 | 必选 | 使用情况 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | 错误 | 指定 <xref:System.ServiceModel.Activities.Receive> 活动的友好名称。 默认值为 Receive。<br /><br /> 虽然对友好 <xref:System.Activities.Activity.DisplayName%2A> 使用非默认值不是绝对必需的，但最好使用非默认值。 |
| <xref:System.ServiceModel.Activities.Receive.OperationName%2A> | 正确 | 指定由此 <xref:System.ServiceModel.Activities.Receive> 活动实现的服务操作的名称。 如果未显式设置 **Action** 属性，则此属性用于构造 **Action** 属性的默认值。 |
| <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> | 错误 | 指定服务协定的名称。 此属性用于将服务操作分组至各个服务协定。 所有具有相同的 <xref:System.ServiceModel.Activities.Receive> 的 <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> 活动都分组到同一服务协定（WSDL 端口类型）中。 默认值是根活动顶级的完全限定 (CLR) 名称。 |
| <xref:System.ServiceModel.Activities.Receive.Content%2A> | 错误 | 指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 通过选择属性网格中"内容"字段旁边的省略号按钮或单击"接收活动设计器"图面上"内容"标签旁边的"定义 **..."** 按钮 **来编辑此属性**。 两者都显示 **"内容定义"** 对话框。 有关如何使用此框的详细信息，请参阅内容 [定义对话框](../workflow-designer/content-definition-dialog-box.md) 主题。 |
| <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> | 错误 | 使用 <xref:System.ServiceModel.Activities.Receive> 对象指定工作流的服务操作中各 <xref:System.ServiceModel.MessageQuerySet> 活动之间的关联。 单击属性网格中属性旁边的省略号 <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> 按钮，打开 **"关联""On 定义"** 对话框。 有关使用此对话框的详细信息，请参阅内容 [定义对话框](../workflow-designer/content-definition-dialog-box.md) 主题。 |
| <xref:System.ServiceModel.Activities.Receive.CorrelatesWith%2A> | 错误 | 指定用于将消息路由到相应工作流实例的 <xref:System.ServiceModel.Activities.CorrelationHandle>。<br /><br /> 单击属性网格中属性旁边的省略号 <xref:System.ServiceModel.Activities.Receive.CorrelatesWith%2A> 按钮，打开" **表达式编辑器"** 对话框。 有关使用此对话框的详细信息，请参阅 [如何：使用表达式编辑器主题](../workflow-designer/how-to-use-the-expression-editor.md) 。 |
| <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> | 错误 | 指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Receive> 对象的集合。 单击属性网格中属性旁边的省略号 <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> 按钮，打开" **添加相关初始值设置项** "对话框。 有关使用此框的详细信息，请参阅添加 [CorrelationInitializers 对话框](../workflow-designer/add-correlationinitializers-dialog-box.md) 主题。 |
| <xref:System.ServiceModel.Activities.Receive.CanCreateInstance%2A> | 错误 | 指定一个值，该值确定如果消息未关联到现有的工作流实例，是否创建一个新工作流实例来处理该消息。 如果值设置为 **true，** 则创建一个新的工作流实例，以在消息与现有工作流实例不相关时处理消息。 |
| <xref:System.ServiceModel.Activities.Receive.KnownTypes%2A> | 错误 | 指定由此 <xref:System.ServiceModel.Activities.Receive> 活动实现的服务操作的已知类型集合。 此属性应与设置为 <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> 的 <xref:System.Runtime.Serialization.DataContractSerializer> 属性结合使用。 如果使用了 <xref:System.Xml.Serialization.XmlSerializer>，则忽略此项。<br /><br /> 选择属性网格中 **KnownTypes** 字段旁边的省略号按钮，以显示"类型集合编辑器"对话框，可以添加相关类型。 有关使用此框的详细信息，请参阅类型 [集合编辑器对话框](../workflow-designer/type-collection-editor-dialog-box.md) 主题。 |
| <xref:System.ServiceModel.Activities.Receive.ProtectionLevel%2A> | 错误 | 指定消息的 <xref:System.Net.Security.ProtectionLevel>。<br /><br /> 1.  <xref:System.Net.Security.ProtectionLevel> 表示仅身份验证。<br />2.  <xref:System.Net.Security.ProtectionLevel> 表示对数据进行签名，以帮助确保传输的数据的完整性。<br />3.  <xref:System.Net.Security.ProtectionLevel> 表示对数据进行加密和签名，以帮助确保传输的数据的机密性和完整性。 |
| <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> | 错误 | 指定 <xref:System.ServiceModel.Activities.Receive> 活动实现的服务操作所使用的序列化程序的类型。 默认值为 <xref:System.Runtime.Serialization.DataContractSerializer>，它使用提供的数据协定将类型实例序列化和反序列化为 XML 流或文档。 如果需要对 XML 进行更多控制，还可使用 <xref:System.Xml.Serialization.XmlSerializer>。 |
| <xref:System.ServiceModel.Activities.Receive.Action%2A> | 错误 | 指定消息的操作标头。 如果未显式设置，则其值默认为 `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}` ：。 |

## <a name="see-also"></a>请参阅

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- 发送
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)
