---
title: 工作流设计器 - Switch&lt;T&gt; 活动设计器
description: 了解如何使用 Switch <T> 活动设计器在工作流设计器中创建和配置 Switch <T> 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.ModelItemKeyValuePair.UI
- System.Activities.Statements.Switch`1.UI
ms.assetid: 18a6c96e-49a9-4356-ab61-fbd7e3ab44bb
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 1fc06eaaa7bd54ff42a087016dae30e674de4023
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666103"
---
# <a name="switcht-activity-designer"></a>Switch\<T> 活动设计器

<xref:System.Activities.Statements.Switch%601> 活动计算指定表达式并执行活动集合中其关联键与计算所得值匹配的活动。

Switch<T\> 活动设计器用于在工作流设计器中创建和配置 <xref:System.Activities.Statements.Switch%601> 活动。

## <a name="the-switchtactivity"></a>Switch\<T>Activity

一个 <xref:System.Activities.Statements.Switch%601> 活动包含一个 <xref:System.Activities.Statements.Switch%601.Expression%2A> 和一个 <xref:System.Activities.Statements.Switch%601.Cases%2A> 的字典。 该字典中的每个事例都包含由一个键和一个用作其对应值的活动组成的对 。 <xref:System.Activities.Statements.Switch%601> 活动计算 <xref:System.Activities.Statements.Switch%601.Expression%2A> 并将其与每个键相比较。 如果找到匹配项，则会执行对应的活动。 只可能有一个匹配项，因为字典键与字典的相等比较器所定义的相等类型的对应必须是唯一的。 如果未找到匹配项，则会执行 <xref:System.Activities.Statements.Switch%601.Default%2A> 活动。

## <a name="how-to-use-the-switcht-activity-designer"></a>如何使用 Switch\<T> 活动设计器

访问“工具箱”的“控制流”类别中的 Switch\<T> 活动设计器  。 将该活动设计器放入工作流设计器中后，它将显示“选择类型”对话框，用户可在其中指定 <xref:System.Activities.Statements.Switch%601> 活动中使用的泛型类型 T。 默认值为 Int32。 选择泛型类型 T 后，Switch<T\> 设计器将添加到工作流设计器中。

下面是 Switch<T\> 设计器的属性。 所有这些属性都可以在属性网格中进行编辑。 其中一些属性还可以在设计器图面上进行编辑。

下表列出最有用的 <xref:System.Activities.Statements.Switch%601> 属性并说明如何在设计器中使用它们。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.Switch%601> 活动设计器的友好名称。 默认值为 Switch<Int32\>。 可以在“属性”窗口或直接在设计器标头中编辑该值。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.Switch%601.Expression%2A>|True|指定用于与 case 集合中的键进行比较以确定执行哪个 case 的表达式。|
|<xref:System.Activities.Statements.Switch%601.Default%2A>||指定未找到匹配项时执行的活动。 单击设计器上的“添加活动”按钮将打开“默认值”框，可在其中放入该活动 。|
|<xref:System.Activities.Statements.Switch%601.Cases%2A>||指定要计算的 case。 若要添加事例，请单击 Switch\<T> 设计器底部的“添加新事例”按钮 。 按钮将变为文本框（如果在添加 Switch\<T> 时选择的泛型类型为 String 或 Enum，则变为组合框）。 在“事例值”框中添加键后，事例区域将展开，可在提示文本“在此处放置活动”处放置活动以定义该事例的执行逻辑。|

可以添加多个 case，但 case 键不能重复。 否则将显示一个错误对话框，报告指定 case 键已存在，您必须选择其他键。 在 Switch\<T> 设计器中，一次只有一个事例区域能以展开的视图显示。 某个 case 区域为折叠的视图时，单击该 case 区域即可展开它。 请注意，对于折叠的 case，如果该活动有显示名称，设计器将在该 case 内的右侧显示该显示名称。 否则将显示“添加活动”按钮，单击该按钮将展开事例，可以在其中添加活动。

单击现有 case 的键可将该键从标签变为文本框，从而可以编辑该 case 键。

删除 case 的方法有两种：

- 选中相应 case，然后删除它。

- 选中相应事例，右键单击以显示上下文菜单，然后选择“删除”。

请注意，必须选中 case 本身才能删除它。 选中并删除 case 内的活动只会删除该活动而不会删除该 case。

## <a name="see-also"></a>另请参阅

- [控制流](../workflow-designer/control-flow-activity-designers.md)
