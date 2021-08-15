---
title: 工作流设计器 - InvokeDelegate
description: 了解 InvokeDelegate 设计器，以及如何使用 InvokeDelegate 设计器创建和配置 InvokeDelegate 活动。
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
ms.openlocfilehash: 12fd42bd51a252470c2b7d4fbae23581847ddf0f6d3dede60f6e2659215d80fd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121393505"
---
# <a name="invokedelegate"></a>InvokeDelegate

**InvokeDelegate** 设计器用于创建和配置 <xref:System.Activities.Statements.InvokeDelegate> 活动。

## <a name="the-invokedelegate-activity"></a>InvokeDelegate 活动

<xref:System.Activities.Statements.InvokeDelegate> 调用公共委托。

### <a name="use-the-invokedelegate-activity-designer"></a>使用 InvokeDelegate 活动设计器

访问"工具箱"的"基元 **"类别中** 的 **InvokeDelegate** 活动 **设计器**。 可以从 **"工具箱"拖动 InvokeDelegate** 活动设计器，工作流设计器放置活动（例如 位于 内）的"对象"图面 <xref:System.Activities.Statements.Sequence> 。 删除活动设计器会创建 <xref:System.Activities.Statements.InvokeDelegate> 默认为 <xref:System.Activities.Activity.DisplayName%2A> InvokeDelegate 的活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在 **InvokeDelegate** 活动设计器的标头或属性网格的 **DisplayName** 框中编辑 。

### <a name="the-invokedelegate-properties"></a>InvokeDelegate 属性

下表列出 <xref:System.Activities.Statements.InvokeDelegate> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中编辑，某些属性可以在工作流设计器编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.InvokeDelegate> 活动的友好名称。 默认值为 InvokeDelegate。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不严格要求 ，但最好使用一个 。|
|<xref:System.Activities.Statements.InvokeDelegate.Delegate%2A>|正确|要在执行活动时调用的 <xref:System.Activities.ActivityDelegate> 的名称。 此属性可以在设计器图面上编辑，并且是必需的。|
|<xref:System.Activities.Statements.InvokeDelegate.DelegateArguments%2A>|错误|调用委托的参数集合。 键是 上的参数对象的名称，值是计算表达式并将其分配给 <xref:System.Activities.ActivityDelegate> 相应参数对象的参数。 若要显示 **可在其中设置此属性的 DelegateArguments** 对话框，请单击属性网格的 **DelegateArguments** 字段中的省略号按钮。 单击" **创建参数** "字段以添加参数。|

## <a name="see-also"></a>另请参阅

- [如何：在工作流设计器中定义和使用活动委托](../workflow-designer/how-to-define-and-consume-activity-delegates-in-the-workflow-designer.md)