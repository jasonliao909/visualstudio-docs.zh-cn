---
title: 工作流设计器 - 发送活动设计器
description: 了解"发送"活动，以及如何使用"发送"活动设计器创建和配置"发送"活动。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122114519"
---
# <a name="send-activity-designer"></a>Send 活动设计器

Send 活动设计器用于创建和配置 <xref:System.ServiceModel.Activities.Send> 活动。

## <a name="the-send-activity"></a>Send 活动

 <xref:System.ServiceModel.Activities.Send> 活动用于向服务发送消息。 作为客户端上请求/响应消息交换模式的一部分接收消息的 <xref:System.ServiceModel.Activities.ReceiveReply> 活动可绑定到 <xref:System.ServiceModel.Activities.Send> 活动。

### <a name="using-the-send-activity-designer"></a>使用 Send 活动设计器

访问 **"工具箱** "的 **"消息传送"类别中** 的"发送" **活动设计器**。 可以将 **"** 发送"活动设计器从"工具箱"拖动到工作流设计器放置活动的位置。 这将创建具有 Send 的默认 <xref:System.ServiceModel.Activities.Send> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在发送活动设计器的标头或属性网格的 **DisplayName** 框中编辑 。

若要创建活动并将其绑定到所选活动，请右键单击"发送活动设计器"，单击上下文菜单中的"创建 <xref:System.ServiceModel.Activities.ReceiveReply> <xref:System.ServiceModel.Activities.Send> **ReceiveReply"** 项 **，ReceiveReplyForSend** 设计器将显示在"发送"设计器 **下方**。 <xref:System.ServiceModel.Activities.ReceiveReply> 活动是作为客户端上请求/响应消息交换模式的一部分接收消息的一个活动。 可以使用 **ReceiveReplyForSend 设计器配置** 它。

或者，"工具箱"的"消息传送"类别中的 **SendAndReceiveReply** 模板设计器可用于创建一对预先配置的 <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.ReceiveReply> 和活动。 有关使用 **SendAndReceiveReply** 和 **ReceiveReplyForSend** 模板的详细信息，请参阅 [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md) 主题。

### <a name="the-send-activity-properties"></a>Send 活动属性

下表列出 <xref:System.ServiceModel.Activities.Send> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中编辑，也可以编辑工作流设计器图面。

| 属性名称 | 必选 | 使用情况 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | 错误 | <xref:System.ServiceModel.Activities.Send> 活动的友好名称。 默认值为 Send。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。 |
| <xref:System.ServiceModel.Activities.Send.OperationName%2A> | 正确 | 由此 <xref:System.ServiceModel.Activities.Send> 活动调用的服务操作的名称。 如果未显式设置 **Action** 属性，则此属性用于构造 **Action** 属性的默认值。 |
| <xref:System.ServiceModel.Activities.Send.ServiceContractName%2A> | 正确 | 实现了要调用的服务的服务协定的名称。 |
| <xref:System.ServiceModel.Activities.Send.Content%2A> | 错误 | 指定要接收的消息或参数内容。 它可为 <xref:System.ServiceModel.Activities.ReceiveMessageContent> 活动或 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 活动。 通过选择属性网格中"内容"字段旁边的省略号按钮或单击"接收活动设计器"图面上"内容"标签旁边的"定义 **..."** 按钮 **来编辑此属性**。 两者都显示 **"内容定义"** 对话框。 有关如何使用此框的详细信息，请参阅内容 [定义对话框](../workflow-designer/content-definition-dialog-box.md) 主题。 |
| <xref:System.ServiceModel.Activities.Send.CorrelatesWith%2A> | 错误 | 指定用于将消息路由到相应工作流实例的 <xref:System.ServiceModel.Activities.CorrelationHandle>。<br /><br /> 单击属性网格中属性旁边的省略号 <xref:System.ServiceModel.Activities.Send.CorrelatesWith%2A> 按钮，打开" **表达式编辑器"** 对话框。 有关使用此对话框的详细信息，请参阅 [如何：使用表达式编辑器主题](../workflow-designer/how-to-use-the-expression-editor.md) 。 |
| <xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A> | 错误 | 指定在工作流中对配置此 <xref:System.ServiceModel.Activities.CorrelationInitializer> 活动的多个 <xref:System.ServiceModel.Activities.CorrelationHandle> 对象进行初始化的 <xref:System.ServiceModel.Activities.Send> 对象的集合。 单击属性网格中属性旁边的省略号 <xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A> 按钮，打开" **添加相关初始值设置项** "对话框。 有关使用此框的详细信息，请参阅添加 [CorrelationInitializers 对话框](../workflow-designer/add-correlationinitializers-dialog-box.md) 主题。 |
| <xref:System.ServiceModel.Activities.Send.KnownTypes%2A> | 错误 | 此 <xref:System.ServiceModel.Activities.Send> 活动要调用的服务操作的已知类型集合。 此属性应与设置为 <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> 的 <xref:System.Runtime.Serialization.DataContractSerializer> 属性结合使用。 如果使用了 <xref:System.Xml.Serialization.XmlSerializer>，则忽略此项。<br /><br /> 选择属性网格中 **KnownTypes** 字段旁边的省略号按钮，以显示"类型集合编辑器"对话框，可以使用该对话框添加相关类型。<br /><br /> 选择属性网格中 **KnownTypes** 字段旁边的省略号按钮，以显示"类型集合编辑器"对话框，可以添加相关类型。 有关使用此框的详细信息，请参阅类型 [集合编辑器对话框](../workflow-designer/type-collection-editor-dialog-box.md) 主题。 |
| <xref:System.ServiceModel.Activities.Send.ProtectionLevel%2A> | 正确 | 指定消息的 <xref:System.Net.Security.ProtectionLevel>。<br /><br /> 1.  <xref:System.Net.Security.ProtectionLevel> 表示仅身份验证。<br />2.  <xref:System.Net.Security.ProtectionLevel> 表示对数据进行签名，以帮助确保传输的数据的完整性。<br />3.  <xref:System.Net.Security.ProtectionLevel> 表示对数据进行加密和签名，以帮助确保传输的数据的机密性和完整性。 |
| <xref:System.ServiceModel.Activities.Send.SerializerOption%2A> | True | <xref:System.ServiceModel.Activities.Send> 活动要调用的服务操作所用的序列化程序。 默认值为 <xref:System.Runtime.Serialization.DataContractSerializer>，它使用提供的数据协定将类型实例序列化和反序列化为 XML 流或文档。 |
| <xref:System.ServiceModel.Activities.Send.Action%2A> | 错误 | 指定消息的操作标头。 如果未显式设置，则其值默认为 `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}` ：。 如果该值是对 <xref:System.ServiceModel.Activities.Send> 活动指定的，则接收消息的 <xref:System.ServiceModel.Activities.Receive> 活动必须具有同一值才能正确传递该消息。 |
| <xref:System.ServiceModel.Activities.Send.TokenImpersonationLevel%2A> | | <xref:System.Security.Principal.TokenImpersonationLevel> 可用于消息的接收方。 它定义安全模拟级别，控制服务器进程可以代表客户端进程执行的程度。<xref:System.Security.Principal.TokenImpersonationLevel>  指示未分配模拟级别。 <xref:System.Security.Principal.TokenImpersonationLevel> 指示服务器进程无法获取有关客户端的标识信息，并且无法模拟客户端。 <xref:System.Security.Principal.TokenImpersonationLevel> 指示服务器进程可以获取有关客户端的信息（如安全标识符和特权）但无法模拟客户端。 这对于导出自身对象的服务器非常有用，例如，导出表和视图的数据库产品。 在不能使用其他正使用客户端安全上下文的服务的情况下，服务器可以使用检索到的客户端安全信息做出访问验证决策。 <xref:System.Security.Principal.TokenImpersonationLevel> 指示服务器进程可以模拟其本地系统上的客户端的安全上下文。 服务器无法在远程系统上模拟客户端。 <xref:System.Security.Principal.TokenImpersonationLevel> 指示服务器进程可以在远程系统上模拟客户端的安全上下文。 |
| <xref:System.ServiceModel.Activities.Send.Endpoint%2A> | | <xref:System.ServiceModel.Endpoint> 活动要将消息发送到的 <xref:System.ServiceModel.Activities.Send>。 如果设置了此属性， <xref:System.ServiceModel.Activities.Send.EndpointConfigurationName%2A> 则属性应为 **null**。 |
| <xref:System.ServiceModel.Activities.Send.EndpointAddress%2A> | | 要将消息发送到的 <xref:System.ServiceModel.EndpointAddress>。 |
| <xref:System.ServiceModel.Activities.Send.EndpointConfigurationName%2A> | | 端点配置的名称。 在配置文件中配置终结点时设置此属性。 此属性应设置为配置文件中的 **\<endpoint>** 元素中提供的名称。 如果设置了此属性，则 <xref:System.ServiceModel.Activities.Send.Endpoint%2A> 属性应为 **null**。 |

## <a name="see-also"></a>请参阅

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [收到](../workflow-designer/receive-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)