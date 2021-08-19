---
title: "\"工作流设计器 CorrelatesOn 定义\" 对话框"
description: 了解如何使用工作流设计器中的 "CorrelatesOn" 对话框编辑 "接收" 活动的 "CorrelatesOn" 属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CorrelatesOnDefinition.UI
ms.assetid: 8b2b627a-f236-4479-aa09-525df65e3413
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 0b0730853bb2f7e67445a85c4a05d6adbfc22dc3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122155260"
---
# <a name="correlateson-definition-dialog-box"></a>“CorrelatesOn 定义”对话框

在工作流设计器中使用 " **CorrelatesOn** " 对话框编辑活动的 <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> 属性 <xref:System.ServiceModel.Activities.Receive> 。 有关详细信息，请参阅 [Receive 活动设计器](../workflow-designer/receive-activity-designer.md)。

<xref:System.ServiceModel.Activities.Receive> 活动之间的关联指定工作流中的不同服务操作如何相互连接。

下表介绍了 " **CorrelatesOn** " 对话框 (UI) 元素的用户界面。

|UI 元素|说明|
|-|-----------------|
|**CorrelatesWith**|用于将消息路由到相应工作流实例的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**XPath 查询**|包含用于从传入消息中提取相关数据的查询的键/值对。 此值与属性相对应 <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> 。 XPath 查询包含在 <xref:System.ServiceModel.MessageQuerySet> 对象中。|

## <a name="to-launch-the-correlateson-dialog-box"></a>启动“CorrelatesOn”对话框

可以将 " **接收** " 活动设计器从 **"工具箱** " 拖放到工作流设计器图面上通常放置活动的任何位置。 删除活动设计器将创建一个 <xref:System.ServiceModel.Activities.Receive> 活动，其中默认为 <xref:System.Activities.Activity.DisplayName%2A> Receive。 若要打开 " **CorrelatesOn 定义** " 对话框，请选择 " **接收** " 活动设计器，然后在属性网格中，选择 **CorrelatesOn** 属性的集合文本旁边的省略号按钮。

## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Activities.Receive>
- [“添加相关初始值设定项”对话框](../workflow-designer/add-correlationinitializers-dialog-box.md)
- [“初始化相关”对话框](../workflow-designer/initialize-correlation-dialog-box.md)