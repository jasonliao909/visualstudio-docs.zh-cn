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
ms.openlocfilehash: aff2353f0ea681935ff576545f6eb14b957f2c1d58136e240917bd4f86653f75
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121440495"
---
# <a name="initializecorrelation-activity-designer"></a>InitializeCorrelation 活动设计器

" **InitializeCorrelation** " 活动设计器用于创建和配置 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活动。 在 <xref:System.ServiceModel.Activities.InitializeCorrelation> 发送或接收消息之前，活动会在消息间建立关联。

## <a name="the-initializecorrelation-activity"></a>InitializeCorrelation 活动

<xref:System.ServiceModel.Activities.InitializeCorrelation> 活动用于在不发送或接收消息的情况下初始化相关。 通常，相关是在发送或接收消息时初始化的。 如果必须在发送或接收消息前建立相关，请使用 <xref:System.ServiceModel.Activities.InitializeCorrelation> 来初始化该相关。

### <a name="using-the-initializecorrelation-activity-designer"></a>使用 InitializeCorrelation 活动设计器

访问 "**工具箱**" 的 "**消息传送**" 类别中的 " **InitializeCorrelation** " 活动设计器。

可以将 " **InitializeCorrelation** " 活动设计器从 " **工具箱** " 拖放到工作流设计器图面上。 删除活动设计器将创建一个 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活动，其默认值为 <xref:System.Activities.Activity.DisplayName%2A> InitializeCorrelation。 <xref:System.Activities.Activity.DisplayName%2A>可以在 " **InitializeCorrelation** " 活动设计器的标头中或在 "**属性**" 窗口的 " **DisplayName** " 框中编辑。

可以在 " <xref:System.ServiceModel.Activities.CorrelationHandle> **InitializeCorrelation** " 活动设计器图面上的 "**属性**" 窗口中的 **相关** 字段中指定。

若要显示 "**初始化相关**" 对话框，在该对话框中可以指定相关句柄和用于初始化它的键值对，请在 "**属性**" 窗口中选择 " **CorrelationData** " 字段旁边的省略号按钮。 或者，选择 "查看 ..." **InitializeCorrelation** 活动设计器图面上的提示文本。 有关使用此对话框的详细信息，请参阅 " [类型集合编辑器" 对话框](../workflow-designer/type-collection-editor-dialog-box.md) 。

### <a name="the-initializecorrelation-properties"></a>InitializeCorrelation 属性

下表显示了 <xref:System.ServiceModel.Activities.InitializeCorrelation> 这些属性，并介绍了如何在设计器中使用它们。 这些属性可以在 " **属性** " 窗口中或工作流设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.ServiceModel.Activities.InitializeCorrelation> 活动的友好名称。 默认值为 InitializeCorrelation。<br /><br /> 尽管不是严格需要为友好使用非默认值 <xref:System.Activities.Activity.DisplayName%2A> ，但建议使用。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.Correlation%2A>|错误|用于关联相关中的工作流活动的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>|错误|将消息与工作流实例相关联的相关数据的字典。<br /><br /> 使用 " **初始化相关** " 对话框可以配置 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> 。 有关使用此对话框的详细信息，请参阅 " [类型集合编辑器" 对话框](../workflow-designer/type-collection-editor-dialog-box.md) 。|

## <a name="see-also"></a>另请参阅

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [收](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- 发送
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)