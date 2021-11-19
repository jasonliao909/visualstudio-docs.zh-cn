---
title: 工作流设计器 - InvokeDelegate
description: 了解 InvokeDelegate 设计器，以及如何使用 InvokeDelegate 设计器来创建和配置 InvokeDelegate 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InvokeDelegate Designer
- System.Activities.Statements.InvokeDelegate.UI
ms.assetid: 289a7498-5127-453f-beb5-05f05b80d26f
author: TerryGLee
ms.author: tglee
ms.workload:
- multiple
ms.openlocfilehash: a482f23b1df1587e9a1c7e3023bfb0d1737f1fae
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126667572"
---
# <a name="invokedelegate"></a>InvokeDelegate

InvokeDelegate 设计器用于创建和配置 <xref:System.Activities.Statements.InvokeDelegate> 活动。

## <a name="the-invokedelegate-activity"></a>InvokeDelegate 活动

<xref:System.Activities.Statements.InvokeDelegate> 调用公共委托。

### <a name="use-the-invokedelegate-activity-designer"></a>使用 InvokeDelegate 活动设计器

访问 InvokeDelegate 活动设计器，其位于工具箱的“基元”类别中  。 可以将 InvokeDelegate 活动设计器从“工具箱”拖放到工作流设计器图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内 。 删除活动设计器将创建一个 <xref:System.Activities.Statements.InvokeDelegate> 活动，其默认的 <xref:System.Activities.Activity.DisplayName%2A> 为“InvokeDelegate”。 可以在 InvokeDelegate 活动设计器的标头中或在属性网格的“DisplayName”框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 。

### <a name="the-invokedelegate-properties"></a>InvokeDelegate 属性

下表列出 <xref:System.Activities.Statements.InvokeDelegate> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在工作流设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.InvokeDelegate> 活动的友好名称。 默认值为 InvokeDelegate。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.InvokeDelegate.Delegate%2A>|True|要在执行活动时调用的 <xref:System.Activities.ActivityDelegate> 的名称。 此属性可以在设计器图面上进行编辑，它是必需的。|
|<xref:System.Activities.Statements.InvokeDelegate.DelegateArguments%2A>|错误|调用委托的参数集合。 键为 <xref:System.Activities.ActivityDelegate> 上的参数对象的名称，值为其表达式将进行计算并分配给对应参数对象的参数。 要显示可在其中设置此属性的“DelegateArguments”对话框，请单击属性窗格的“DelegateArguments”字段中的省略号按钮 。 单击“创建参数”字段以添加参数。|

## <a name="see-also"></a>另请参阅

- [如何：在工作流设计器中定义和使用活动委托](../workflow-designer/how-to-define-and-consume-activity-delegates-in-the-workflow-designer.md)