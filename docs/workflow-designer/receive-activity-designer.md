---
title: 工作流设计器 - Receive 活动设计器
description: 了解 Receive 活动，以及如何使用 Receive 活动设计器来创建和配置 Receive 活动。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665904"
---
# <a name="receive-activity-designer"></a>Receive 活动设计器

Receive 活动设计器用于创建和配置 <xref:System.ServiceModel.Activities.Receive> 活动。 <xref:System.ServiceModel.Activities.Receive> 活动是接收消息的活动，可接收的消息包括内置类型（如 <xref:System.ServiceModel.Channels.Message>、<xref:System.IO.Stream> 或 <xref:System.Xml.Linq.XElement>）或者应用程序定义的数据协定、消息协定或可序列化的 XML 类。

## <a name="the-receive-activity"></a>Receive 活动

<xref:System.ServiceModel.Activities.Receive> 活动可以接收一个或多个项，具体取决于所用接收内容的类型。 <xref:System.ServiceModel.Activities.SendReply> 活动可绑定到作为服务上请求/响应消息交换模式的一部分接收消息的 <xref:System.ServiceModel.Activities.Receive> 活动。

### <a name="using-the-receive-activity-designer"></a>使用 Receive 活动设计器

访问“工具箱”的“消息”类别中的 Receive 活动设计器  。 可以将 Receive 活动设计器从“工具箱”拖动到工作流设计器图面上通常放置活动的任何位置 。 这将创建具有 Receive 的默认 <xref:System.ServiceModel.Activities.Receive> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 可以在 Receive 活动设计器的标头中或在属性网格的“DisplayName”框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 。

若要创建 <xref:System.ServiceModel.Activities.SendReply> 活动并将其绑定到所选 <xref:System.ServiceModel.Activities.Receive> 活动，请右键单击 Receive 活动设计器，然后在上下文菜单中单击“创建 SendReply”项，此时 SendReplyToReceive 设计器将显示在 Receive 设计器下   。 <xref:System.ServiceModel.Activities.SendReply> 活动是作为服务上请求/响应消息交换模式的一部分发送答复消息的一个活动。 它可通过 SendReplyToReceive 设计器进行配置。

或者，可使用“工具箱”的“消息”类别中的 ReceiveAndSendReply 模板设计器创建一对预配置的 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动  。 有关 ReceiveAndSendReply 和 SendReplyToReceive 模板用法的详细信息，请参阅 [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md) 主题 。

### <a name="the-receive-activity-properties"></a>Receive 活动属性

下表列出 <xref:System.ServiceModel.Activities.Receive> 属性并说明如何在设计器中使用它们。 可以在“属性”网格中或在工作流设计器图面上编辑这些属性。 唯一必需的属性是 <xref:System.ServiceModel.Activities.Receive.OperationName%2A> 属性。

| 属性名称 | 必选 | 使用情况 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | 错误 | 指定 <xref:System.ServiceModel.Activities.Receive> 活动的友好名称。 默认值为 Receive。<br /><br /> 虽然对友好 <xref:System.Activities.Activity.DisplayName%2A> 使用非默认值不是绝对必需的，但最好使用非默认值。 |
| <xref:System.ServiceModel.Activities.Receive.OperationName%2A> | True | 指定由此 <xref:System.ServiceModel.Activities.Receive> 活动实现的服务操作的名称。 如果未显式设置 Action 属性，则此属性将用于构造 Action 属性的默认值 。 |
| <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> | 错误 | 指定服务协定的名称。 此属性用于将服务操作分组至各个服务协定。 所有具有相同的 <xref:System.ServiceModel.Activities.Receive> 的 <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> 活动都分组到同一服务协定（WSDL 端口类型）中。 默认值为顶级（根）活动的完全限定的 CLR 名称。 |
| <xref:System.ServiceModel.Activities.Receive.Content%2A> | 错误 | 指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 编辑此属性的方法是选择属性网格中“内容”字段旁的省略号按钮，或单击 Receive 活动设计器图面上“内容”标签旁的“定义…”按钮   。 两者都显示“内容定义”对话框。 有关如何使用此框的详细信息，请参阅[“内容定义”对话框](../workflow-designer/content-definition-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> | 错误 | 使用 <xref:System.ServiceModel.Activities.Receive> 对象指定工作流的服务操作中各 <xref:System.ServiceModel.MessageQuerySet> 活动之间的关联。 单击属性网格中 <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> 属性旁边的省略号按钮，以打开“CorrelatesOn 定义”对话框。 有关如何使用此对话框的详细信息，请参阅[“内容定义”对话框](../workflow-designer/content-definition-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.Receive.CorrelatesWith%2A> | 错误 | 指定用于将消息路由到相应工作流实例的 <xref:System.ServiceModel.Activities.CorrelationHandle>。<br /><br /> 单击属性网格中 <xref:System.ServiceModel.Activities.Receive.CorrelatesWith%2A> 属性旁边的省略号按钮，以打开“表达式编辑器”对话框。 有关如何使用此对话框的详细信息，请参阅[如何：使用表达式编辑器](../workflow-designer/how-to-use-the-expression-editor.md)主题。 |
| <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> | 错误 | 指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Receive> 对象的集合。 单击属性网格中 <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> 属性旁边的省略号按钮，以打开“添加相关初始值设定项”对话框。 有关如何使用此框的详细信息，请参阅[“添加相关初始值设定项”对话框](../workflow-designer/add-correlationinitializers-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.Receive.CanCreateInstance%2A> | 错误 | 指定一个值，该值确定如果消息未关联到现有的工作流实例，是否创建一个新工作流实例来处理该消息。 如果该值设置为 true，则当消息未关联到现有工作流实例时将创建一个新工作流实例来处理该消息。 |
| <xref:System.ServiceModel.Activities.Receive.KnownTypes%2A> | 错误 | 指定由此 <xref:System.ServiceModel.Activities.Receive> 活动实现的服务操作的已知类型集合。 此属性应与设置为 <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> 的 <xref:System.Runtime.Serialization.DataContractSerializer> 属性结合使用。 如果使用了 <xref:System.Xml.Serialization.XmlSerializer>，则忽略此项。<br /><br /> 选择属性网格中“KnownTypes”字段旁的省略号按钮可显示“类型集合编辑器”对话框，使用该对话框可添加相关类型 。 有关如何使用此框的详细信息，请参阅[“类型集合编辑器”对话框](../workflow-designer/type-collection-editor-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.Receive.ProtectionLevel%2A> | 错误 | 指定消息的 <xref:System.Net.Security.ProtectionLevel>。<br /><br /> 1. <xref:System.Net.Security.ProtectionLevel> 表示仅进行身份验证。<br />2. <xref:System.Net.Security.ProtectionLevel> 表示对数据进行签名以帮助确保所传输数据的完整性。<br />3. <xref:System.Net.Security.ProtectionLevel> 表示对数据进行加密和签名以帮助确保所传输数据的保密性和完整性。 |
| <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> | 错误 | 指定 <xref:System.ServiceModel.Activities.Receive> 活动实现的服务操作所使用的序列化程序的类型。 默认值为 <xref:System.Runtime.Serialization.DataContractSerializer>，它使用提供的数据协定将类型实例序列化和反序列化为 XML 流或文档。 如果需要对 XML 进行更多控制，还可使用 <xref:System.Xml.Serialization.XmlSerializer>。 |
| <xref:System.ServiceModel.Activities.Receive.Action%2A> | 错误 | 指定消息的操作标头。 如果未显式设置，则它的默认值为：`https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}`。 |

## <a name="see-also"></a>另请参阅

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- 发送
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)
