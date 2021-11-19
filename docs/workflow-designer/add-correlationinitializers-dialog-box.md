---
title: “添加 CorrelationInitializers”对话框
description: 了解如何使用工作流设计器中的“添加相关初始值设定项”对话框来配置 Send、Receive 和 SendReply 活动的 CorrelationInitializers 属性。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664914"
---
# <a name="add-correlationinitializers-dialog-box"></a>“添加相关初始值设定项”对话框

工作流设计器中的“添加相关初始值设定项”对话框用于配置 <xref:System.ServiceModel.Activities.Send>、<xref:System.ServiceModel.Activities.Receive>、<xref:System.ServiceModel.Activities.SendReply> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 活动的 CorrelationInitializers 属性 。 有关使用此框的活动设计器的详细信息，请参阅 [Send](../workflow-designer/send-activity-designer.md)、[Receive](../workflow-designer/receive-activity-designer.md)、[ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md) 和 [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md) 主题。

通过此对话框指定的集合中的相关初始值设置项可以初始化消息传送活动之间的以下关联：

- 基于查询
- 上下文
- 回调上下文
- 请求-答复

下表描述“添加相关初始值设定项”对话框的用户界面 (UI) 元素：

|UI 元素|说明|
|-|-----------------|
|**添加初始值设定项**|单击“添加初始值设定项”框可将其他初始值设定项添加到集合中。|
|**相关性类型**|指定相关初始值设定项的类型。 有四种类型可供选择：<br /><br /> 1. 用于指定 <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer> 的回调相关初始值设定项。<br />2. 用于指定 <xref:System.ServiceModel.Activities.CorrelationInitializer> 的上下文相关初始值设定项。<br />3. 用于指定 <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> 的请求-答复相关初始值设定项。<br />4. 用于指定 <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 的查询相关初始值设定项。<br /><br /> 编辑“CorrelationType”<br /><br /> 1. 使用 Tab 键移动到“添加初始值设定项”数据网格中的特定行。<br />2. 若要将焦点置于 CorrelationTypeComboBox，请按“Ctrl+Tab”  。<br />3. 按“Alt+Down”弹出 ComboBox，然后对其进行编辑。|
|**XPath 查询**|包含用于从传入和传出消息中提取相关数据的查询的键/值对。 仅当使用 <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 类型时此列表才有效。|

## <a name="to-launch-the-add-correlation-initializers-dialog-box"></a>启动“添加相关初始值设定项”对话框

 “添加相关初始值设定项”对话框由“Send”、“Receive”、“ReceiveAndSendReply”和“SendAndReceiveReply”设计器使用    。 在任何情况下访问它们的方式都相同，此处使用“Receive”设计器的用例来说明该过程。

 可以将“Receive”活动设计器从“工具箱”拖放到工作流设计器图面上放置活动的任何位置 。 删除“Receive”活动设计器将创建一个 <xref:System.ServiceModel.Activities.Receive> 活动，其默认 <xref:System.Activities.Activity.DisplayName%2A> 为 Receive。 选择“Receive”活动设计器，然后在属性网格中单击“CorrelationInitializers”属性的（集合）文本旁的省略号按钮，以显示“添加相关初始值设定项”对话框  。

## <a name="see-also"></a>另请参阅

- [“初始化相关”对话框](../workflow-designer/initialize-correlation-dialog-box.md)
