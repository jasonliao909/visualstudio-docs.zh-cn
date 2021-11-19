---
title: 工作流设计器 - 内容定义对话框
description: 了解如何使用"内容定义"对话框配置 Send、Receive、SendReply 和 ReceiveReply 活动的 Content 属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MessageContent.UI
ms.assetid: 7e4237c3-90a1-4149-bd8a-3643d1dde0df
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: b3432853ce9e6aaf4f37c4a0c363099f4a61d988
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602192"
---
# <a name="content-definition-dialog-box"></a>“内容定义”对话框

" **内容定义** "对话框用于工作流设计器、、 和 活动的 **Content** <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.Receive> <xref:System.ServiceModel.Activities.SendReply> <xref:System.ServiceModel.Activities.ReceiveReply> 属性。 有关使用此框的活动设计器详细信息，请参阅发送、接收[、ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)和[SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)主题。 [](../workflow-designer/send-activity-designer.md) [](../workflow-designer/receive-activity-designer.md)

下表介绍了"初始化关联" (用户界面) **元素的用户界面** ：

|UI 元素|说明|
|-|-----------------|
|**消息**|使用"消息类型"下拉列表框，使用"消息 **数据** 表达式"文本框和类型指定消息内容。 默认情况下， **内容定义** 使用 ，它要求工作流服务定义中的 <xref:System.ServiceModel.Activities.ReceiveMessageContent> <xref:System.ServiceModel.Channels.Message> 或消息协定类型。|
|**Parameters**|单击 **"参数"** 单选按钮以 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 使用 需要数据协定的 。 使用数据网格设置 <xref:System.Activities.OutArgument> 键/值对的泛型集合，这些键/值对的值将赋给当前工作流中的可变参数。|

"**内容定义**"对话框由Send、Receive、ReceiveAndSendReply 和 **SendAndReceiveReply 设计器** 使用。   在任何情况下访问它们的方式都相同，此处使用“Receive”设计器来演示该过程。

可以 **拖动"** 接收"活动设计器，将其从"工具箱"拖放到工作流设计器放置活动的位置。 这将创建具有 Receive 的默认 <xref:System.ServiceModel.Activities.Receive> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 选择"**接收**"活动设计器，然后单击"内容定义"对话框 (网格中"内容"属性) 文本旁边的省略号按钮。 

可以在活动的"消息 **"部分或** 活动的" <xref:System.ServiceModel.Activities.ReceiveMessageContent> **参数"** 部分中指定 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 内容。

## <a name="see-also"></a>另请参阅

- [工作流设计器 UI 帮助](browse-and-select-a-dotnet-type-dialog-box.md)