---
title: 工作流设计器 - InvokeMethod 活动设计器
description: 了解 InvokeMethod 活动，以及如何使用 InvokeMethod 活动设计器创建和配置 InvokeMethod 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.InvokeMethod.UI
ms.assetid: 15e6efdc-52ca-46d8-9c5e-063f7c8265a6
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: b070da362b84aa7e258ad6ecd628ea524e4a9b3daf7abd06118b783399c2baa9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121314246"
---
# <a name="invokemethod-activity-designer"></a>InvokeMethod 活动设计器

**InvokeMethod** 设计器用于创建和配置 <xref:System.Activities.Statements.InvokeMethod> 活动。

## <a name="the-invokemethod-activity"></a>InvokeMethod 活动

<xref:System.Activities.Statements.InvokeMethod> 调用指定对象或类型的公共方法。

### <a name="use-the-invokemethod-activity-designer"></a>使用 InvokeMethod 活动设计器

访问"工具箱"的"基元 **"类别中** 的 **InvokeMethod** 活动 **设计器**。 可以从 **"工具箱"拖动 InvokeMethod** 活动设计器，并拖放到工作流设计器放置活动（例如 位于 内）的图面 <xref:System.Activities.Statements.Sequence> 。 删除活动设计器会创建 <xref:System.Activities.Statements.InvokeMethod> 默认为 <xref:System.Activities.Activity.DisplayName%2A> InvokeMethod 的活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在 **InvokeMethod** 活动设计器的标头或属性网格的 **DisplayName** 框中编辑 。

### <a name="the-invokemethod-properties"></a>InvokeMethod 属性

下表显示了 <xref:System.Activities.Statements.InvokeMethod> 属性，并介绍了如何在设计器中使用这些属性。 这些属性可以在属性网格中编辑，某些属性可以在工作流设计器编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.InvokeMethod> 活动的友好名称。 默认值为 InvokeMethod。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不严格要求 ，但最好使用一个 。|
|<xref:System.Activities.Statements.InvokeMethod.MethodName%2A>|正确|要在执行活动时调用的方法的名称。 调用的方法必须声明为 **公共**。 此属性可以在设计器图面上编辑，并且是必需的。|
|<xref:System.Activities.Statements.InvokeMethod.Parameters%2A>|错误|所调用方法的参数集合。 将参数添加到集合中的顺序必须与这些参数在方法签名中出现的顺序相同。 若要显示 **可在其中** 设置此属性的"参数"对话框，请单击属性网格的" **参数** "字段中的省略号按钮。 单击" **创建参数** "按钮以添加参数。|
|<xref:System.Activities.Statements.InvokeMethod.Result%2A>|错误|方法调用的返回值。|
|<xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A>|正确|指定是否异步调用该方法。 默认值为 **False**。|
|<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>|错误|包含要调用的方法的对象。 此属性可以在设计器图面上进行编辑。<br /><br /> 必须设置 <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> 或 <xref:System.Activities.Statements.InvokeMethod.TargetType%2A> 之一。|
|<xref:System.Activities.Statements.InvokeMethod.TargetType%2A>|错误|<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> 的类型。 此属性可以在设计器图面上进行编辑。 只有当调用的方法为静态时，才必须设置此属性。|

若要将参数作为 C# **out** 参数传递 (例如 ，请使用 `Method1(out myParam))` **OutArgument** 而不是 **InOutArgument**

不能使用 活动调用具有 **名为 TargetObject** 或 **Result** 的参数 <xref:System.Activities.Statements.InvokeMethod> 的方法。 原因是 <xref:System.Activities.Statements.InvokeMethod> 活动在 <xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A> 中注册 <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>、<xref:System.Activities.Statements.InvokeMethod.Result%2A> 和 <xref:System.Activities.Activity.CacheMetadata%2A>。

在 <xref:System.Activities.Activity.CacheMetadata%2A> 中注册这些参数的算法如下所列：

1. 注册 <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> 自变量。

2. 注册 <xref:System.Activities.Statements.InvokeMethod.Result%2A> 自变量。

3. 循环访问 <xref:System.Activities.Statements.InvokeMethod.Parameters%2A> 集合并注册每个自变量。

产生的异常的类型为 <xref:System.Activities.InvalidWorkflowException> 并带有以下消息：“InvokeMethod”: 已存在名为“TargetObject”的变量、RuntimeArgument 或 DelegateArgument。 在环境作用域中，名称必须唯一。

此限制不适用于 <xref:System.Activities.Statements.InvokeMethod.TargetType%2A> 和 <xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A> 。 它们不是工作流参数，因此不会在 方法中的 <xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A> <xref:System.Activities.Statements.InvokeMethod> 活动集合中 <xref:System.Activities.Activity.CacheMetadata%2A> 注册。

## <a name="see-also"></a>另请参阅

- [基元](../workflow-designer/primitives-activity-designers.md)
- [Assign](../workflow-designer/assign-activity-designer.md)
- [延迟](../workflow-designer/delay-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)
