---
title: 工作流设计器 -“初始化相关”对话框
description: 了解如何使用工作流设计器中的“初始化相关”对话框来编辑 InitializeCorrelation 活动的 CorrelationData 属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InitializeCorrelation.UI
ms.assetid: 2a0a1cd3-7b9e-493e-9264-fcf85289ffcf
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 391ff86b47b766b01066913b492d4f963361d49c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666111"
---
# <a name="initialize-correlation-dialog-box"></a>“初始化相关”对话框

“初始化相关”对话框在工作流设计器中用于编辑 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活动的 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> 属性。 有关详细信息，请参阅 [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)。

下表描述“初始化相关”对话框的用户界面 (UI) 元素：

|UI 元素|说明|
|-|-----------------|
|**相关性**|要初始化的相关的 <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**初始化开**|一个键/值对，包含要初始化的数据。 此值与 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> 属性相对应。 有效键/值对的一个示例是名为“OrderID”的键与名为“OrderID”的变量配对。|

## <a name="to-launch-the-initialize-correlation-dialog-box"></a>启动“初始化相关”对话框

在“InitializeCorrelation”活动设计器上单击“查看”，或在工作流设计器中选择一个 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活动 。 然后，在属性网格中单击 <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> 属性旁的省略号按钮。

## <a name="see-also"></a>另请参阅

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
