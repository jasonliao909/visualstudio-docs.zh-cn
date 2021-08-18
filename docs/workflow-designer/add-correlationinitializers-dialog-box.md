---
title: "\"添加 CorrelationInitializers\"对话框"
description: 了解如何使用 工作流设计器 中的"添加相关初始值设定项"对话框来配置 Send、Receive 和 SendReply 活动的 CorrelationInitializers 属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AddCorrelationInitializers.UI
ms.assetid: c0517467-d54a-4ee6-aef0-c19b96b6f395
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 4085d8536c9d8f15e8928e010bb2744551a7747c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122099303"
---
# <a name="add-correlationinitializers-dialog-box"></a>“添加相关初始值设定项”对话框

" **添加相关初始值** 设定项"对话框用于工作流设计器、、 和 活动的 **CorrelationInitializers** <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.Receive> <xref:System.ServiceModel.Activities.SendReply> <xref:System.ServiceModel.Activities.ReceiveReply> 属性。 有关使用此框的活动设计器详细信息，请参阅发送、接收[、ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)和[SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)主题。 [](../workflow-designer/send-activity-designer.md) [](../workflow-designer/receive-activity-designer.md)

通过此对话框指定的集合中的相关初始值设置项可以初始化消息传送活动之间的以下关联：

- 基于查询
- 上下文
- 回调上下文
- request-reply

下表介绍了"添加关联初始值 (") UI **的** 用户界面：

|UI 元素|说明|
|-|-----------------|
|**添加初始值设定项**|单击" **添加初始化"** 框，向集合添加其他初始值设置项。|
|**相关类型**|指定相关初始值设定项的类型。 有四种类型可供选择：<br /><br /> 1.用于指定 的回调关联初始值设置项 <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer> 。<br />2.用于指定 的上下文相关初始值设置项 <xref:System.ServiceModel.Activities.CorrelationInitializer> 。<br />3.用于指定 的请求-答复相关初始值设置项 <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> 。<br />4.用于指定 的查询关联初始值表达式 <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 。<br /><br /> 编辑 **CorrelationType**<br /><br /> 1.在"添加初始值设置项 DataGrid"中按 Tab **键到** 特定行。<br />2.若要将焦点设置为 **CorrelationTypeComboBox，** 请按 **Ctrl** + **Tab**。<br />3.按 Alt+Down 弹出 **ComboBox** 并对其进行编辑。|
|**XPath 查询**|包含用于从传入和传出消息中提取相关数据的查询的键/值对。 仅当使用 <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 类型时此列表才有效。|

## <a name="to-launch-the-add-correlation-initializers-dialog-box"></a>启动“添加相关初始值设定项”对话框

 Send、Receive、ReceiveAndSendReply 和 **SendAndReceiveReply** 设计器使用"添加相关初始值设置程序"对话框。    在每种情况下访问它们都是类似的，此处使用"接收"设计器的用例来说明该过程。

 可以 **拖动"** 接收"活动设计器，将其从"工具箱"拖放到工作流设计器放置活动的位置。 删除 **Receive** 活动设计器会创建 <xref:System.ServiceModel.Activities.Receive> 一个默认为 <xref:System.Activities.Activity.DisplayName%2A> Receive 的活动。 选择 **"接收**"活动设计器，然后单击属性网格中"添加相关初始值设置程序"对话框的" (Collection) "属性旁边的省略号按钮。  

## <a name="see-also"></a>请参阅

- [“初始化相关”对话框](../workflow-designer/initialize-correlation-dialog-box.md)
