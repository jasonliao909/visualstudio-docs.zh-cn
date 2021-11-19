---
title: 工作流设计器 - Send 活动设计器
description: 了解 Send 活动，查看如何使用 Send 活动设计器来创建和配置 Send 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.Send.UI
ms.assetid: b514f2e4-767c-4b94-ac61-dd3a54d4b96d
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 1574d6b48e904288cde5ea66be6350430b81bc44
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666974"
---
# <a name="send-activity-designer"></a>Send 活动设计器

Send 活动设计器用于创建和配置 <xref:System.ServiceModel.Activities.Send> 活动。

## <a name="the-send-activity"></a>Send 活动

 <xref:System.ServiceModel.Activities.Send> 活动用于向服务发送消息。 作为客户端上请求/响应消息交换模式的一部分接收消息的 <xref:System.ServiceModel.Activities.ReceiveReply> 活动可绑定到 <xref:System.ServiceModel.Activities.Send> 活动。

### <a name="using-the-send-activity-designer"></a>使用 Send 活动设计器

在“工具箱”的“消息”类别中访问 Send 活动设计器  。 可将 Send 活动设计器从“工具箱”拖放到工作流设计器图面上通常放置活动的任何位置 。 这将创建具有 Send 的默认 <xref:System.ServiceModel.Activities.Send> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 可在 Send 活动设计器的标头中或在属性网格的“DisplayName”框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 。

若要创建 <xref:System.ServiceModel.Activities.ReceiveReply> 活动并将其绑定到所选的 <xref:System.ServiceModel.Activities.Send> 活动，请右键单击 Send 活动设计器，然后在上下文菜单中单击“创建 ReceiveReply”项，此时 Send 设计器下会显示 ReceiveReplyForSend 设计器   。 <xref:System.ServiceModel.Activities.ReceiveReply> 活动是作为客户端上请求/响应消息交换模式的一部分接收消息的一个活动。 可通过 ReceiveReplyForSend 设计器配置它。

或者，可使用“工具箱”的“消息”类别中的 SendAndReceiveReply 模板设计器来创建一对预配置的 <xref:System.ServiceModel.Activities.Send> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 活动  。 若要详细了解如何使用 SendAndReceiveReply 和 ReceiveReplyForSend 模板，请参阅 [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md) 主题 。

### <a name="the-send-activity-properties"></a>Send 活动属性

下表列出 <xref:System.ServiceModel.Activities.Send> 属性并说明如何在设计器中使用它们。 可在属性网格中或工作流设计器图面上编辑这些属性。

| 属性名称 | 必选 | 使用情况 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | 错误 | <xref:System.ServiceModel.Activities.Send> 活动的友好名称。 默认值为 Send。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。 |
| <xref:System.ServiceModel.Activities.Send.OperationName%2A> | True | 由此 <xref:System.ServiceModel.Activities.Send> 活动调用的服务操作的名称。 如果未显式设置 Action 属性，则此属性用于构造 Action 属性的默认值 。 |
| <xref:System.ServiceModel.Activities.Send.ServiceContractName%2A> | True | 实现了要调用的服务的服务协定的名称。 |
| <xref:System.ServiceModel.Activities.Send.Content%2A> | 错误 | 指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 可选择属性网格中“内容”字段旁的省略号按钮，或者单击 Receive 活动设计器图面上“内容”标签旁的“定义…”按钮来编辑此属性   。 这两者都会显示“内容定义”对话框。 若要详细了解如何使用此框，请参阅[“内容定义”对话框](../workflow-designer/content-definition-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.Send.CorrelatesWith%2A> | 错误 | 指定用于将消息路由到相应工作流实例的 <xref:System.ServiceModel.Activities.CorrelationHandle>。<br /><br /> 在属性网格中单击 <xref:System.ServiceModel.Activities.Send.CorrelatesWith%2A> 属性旁边的省略号按钮，打开“表达式编辑器”对话框。 若要详细了解如何使用此对话框，请参阅[如何：使用表达式编辑器](../workflow-designer/how-to-use-the-expression-editor.md)主题。 |
| <xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A> | 错误 | 指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Send> 对象的集合。 在属性网格中单击 <xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A> 属性旁边的省略号按钮，打开“添加相关初始值设定项”对话框。 若要详细了解如何使用此框，请参阅[“添加相关初始值设定项”对话框](../workflow-designer/add-correlationinitializers-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.Send.KnownTypes%2A> | 错误 | 此 <xref:System.ServiceModel.Activities.Send> 活动要调用的服务操作的已知类型集合。 此属性应与设置为 <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> 的 <xref:System.Runtime.Serialization.DataContractSerializer> 属性结合使用。 如果使用了 <xref:System.Xml.Serialization.XmlSerializer>，则忽略此项。<br /><br /> 在属性网格中选择“KnownTypes”字段旁的省略号按钮调出“类型集合编辑器”对话框，可在这里添加相关类型 。<br /><br /> 在属性网格中选择“KnownTypes”字段旁的省略号按钮调出“类型集合编辑器”对话框，可在这里添加相关类型 。 若要详细了解如何使用此框，请参阅[“类型集合编辑器”对话框](../workflow-designer/type-collection-editor-dialog-box.md)主题。 |
| <xref:System.ServiceModel.Activities.Send.ProtectionLevel%2A> | True | 指定消息的 <xref:System.Net.Security.ProtectionLevel>。<br /><br /> 1. <xref:System.Net.Security.ProtectionLevel> 表示仅进行身份验证。<br />2. <xref:System.Net.Security.ProtectionLevel> 表示对数据签名来帮助确保传输的数据的完整性。<br />3. <xref:System.Net.Security.ProtectionLevel> 表示对数据进行加密和签名来帮助确保传输的数据的保密性和完整性。 |
| <xref:System.ServiceModel.Activities.Send.SerializerOption%2A> | True | <xref:System.ServiceModel.Activities.Send> 活动要调用的服务操作所用的序列化程序。 默认值为 <xref:System.Runtime.Serialization.DataContractSerializer>，它使用提供的数据协定将类型实例序列化和反序列化为 XML 流或文档。 |
| <xref:System.ServiceModel.Activities.Send.Action%2A> | 错误 | 指定消息的操作标头。 如果未显式设置，则它的默认值为：`https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}`。 如果该值是对 <xref:System.ServiceModel.Activities.Send> 活动指定的，则接收消息的 <xref:System.ServiceModel.Activities.Receive> 活动必须具有同一值才能正确传递该消息。 |
| <xref:System.ServiceModel.Activities.Send.TokenImpersonationLevel%2A> | | <xref:System.Security.Principal.TokenImpersonationLevel> 可用于消息的接收方。 它会定义安全模拟级别，这控制服务器进程可在何种程度上代表客户端进程执行操作。<xref:System.Security.Principal.TokenImpersonationLevel>  指示未分配模拟级别。 <xref:System.Security.Principal.TokenImpersonationLevel> 指示服务器进程无法获取客户端的标识信息且无法模拟客户端。 <xref:System.Security.Principal.TokenImpersonationLevel> 指示服务器进程可获取客户端的相关信息（如安全标识符和权限），但它无法模拟客户端。 这对于导出自身对象的服务器非常有用，例如，导出表和视图的数据库产品。 在不能使用其他正使用客户端安全上下文的服务的情况下，服务器可以使用检索到的客户端安全信息做出访问验证决策。 <xref:System.Security.Principal.TokenImpersonationLevel> 指示服务器进程可在其本地系统上模拟客户端的安全上下文。 服务器无法在远程系统上模拟客户端。 <xref:System.Security.Principal.TokenImpersonationLevel> 指示服务器进程可在远程系统上模拟客户端的安全上下文。 |
| <xref:System.ServiceModel.Activities.Send.Endpoint%2A> | | <xref:System.ServiceModel.Endpoint> 活动要将消息发送到的 <xref:System.ServiceModel.Activities.Send>。 如果设置了此属性，则 <xref:System.ServiceModel.Activities.Send.EndpointConfigurationName%2A> 属性应为 NULL。 |
| <xref:System.ServiceModel.Activities.Send.EndpointAddress%2A> | | 要将消息发送到的 <xref:System.ServiceModel.EndpointAddress>。 |
| <xref:System.ServiceModel.Activities.Send.EndpointConfigurationName%2A> | | 端点配置的名称。 在配置文件中配置终结点时设置此属性。 此属性应设置为配置文件中 \<endpoint> 元素中给定的名称。 如果设置了此属性，则 <xref:System.ServiceModel.Activities.Send.Endpoint%2A> 属性应为 NULL。 |

## <a name="see-also"></a>另请参阅

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [Receive](../workflow-designer/receive-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)