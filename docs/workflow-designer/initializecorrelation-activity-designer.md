---
title: InitializeCorrelation 活动设计器
description: 在工作流设计器中，了解如何使用 InitializeCorrelation 活动设计器创建和配置 InitializeCorrelation 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.InitializeCorrelation.UI
ms.assetid: 4c54f34c-ee84-42a6-abb0-ec260c1ccb76
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 71756f4ed01253607efae47193ea8ddaa6b52a75
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122130437"
---
# <a name="initializecorrelation-activity-designer"></a>InitializeCorrelation 活动设计器

**InitializeCorrelation** 活动设计器用于创建和配置 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活动。 活动 <xref:System.ServiceModel.Activities.InitializeCorrelation> 在发送或接收消息之前在消息之间建立关联。

## <a name="the-initializecorrelation-activity"></a>InitializeCorrelation 活动

<xref:System.ServiceModel.Activities.InitializeCorrelation> 活动用于在不发送或接收消息的情况下初始化相关。 通常，相关是在发送或接收消息时初始化的。 如果必须在发送或接收消息前建立相关，请使用 <xref:System.ServiceModel.Activities.InitializeCorrelation> 来初始化该相关。

### <a name="using-the-initializecorrelation-activity-designer"></a>使用 InitializeCorrelation 活动设计器

访问"工具箱"的"消息"类别中的 **InitializeCorrelation** 活动 **设计器**。

可以从 **工具箱拖动 InitializeCorrelation** 活动设计器，并拖放到工作流设计器图面。 删除活动设计器会创建 <xref:System.ServiceModel.Activities.InitializeCorrelation> 一个默认为 <xref:System.Activities.Activity.DisplayName%2A> InitializeCorrelation 的活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在 **InitializeCorrelation** 活动设计器的标头中或在"属性"窗口的 **"DisplayName"** 框中 **编辑**。

可以在 <xref:System.ServiceModel.Activities.CorrelationHandle> **InitializeCorrelation** 活动设计器图面上 **的"属性"** 窗口中的"相关"字段中指定 。 

若要显示 **"初始化相关** "对话框，可在其中指定相关句柄和用于初始化它的键值对，请选择"属性"窗口中 **"CorrelationData"** 字段旁边的 **省略号按钮** 。 或者，选择"查看..." **InitializeCorrelation 活动设计器图面上的** 提示文本。 有关使用此对话框的详细信息，请参阅类型 [集合编辑器对话框一](../workflow-designer/type-collection-editor-dialog-box.md) 文。

### <a name="the-initializecorrelation-properties"></a>InitializeCorrelation 属性

下表显示了 <xref:System.ServiceModel.Activities.InitializeCorrelation> 属性，并介绍了如何在设计器中使用这些属性。 这些属性可以在"属性"窗口中 **或** 工作流设计器编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.ServiceModel.Activities.InitializeCorrelation> 活动的友好名称。 默认值为 InitializeCorrelation。<br /><br /> 虽然不严格要求使用友好项的非 <xref:System.Activities.Activity.DisplayName%2A> 默认值，但建议这样做。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.Correlation%2A>|错误|用于关联相关中的工作流活动的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>|错误|将消息与工作流实例相关联的相关数据的字典。<br /><br /> 使用 **"初始化相关** " 对话框可以配置 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> 。 有关使用此对话框的详细信息，请参阅类型 [集合编辑器对话框一](../workflow-designer/type-collection-editor-dialog-box.md) 文。|

## <a name="see-also"></a>请参阅

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [收到](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- 发送
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)