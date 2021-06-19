---
title: 响应并传播更改
description: 了解创建、删除或更新元素时，可以编写将更改传播到模型的其他部分或外部资源的代码。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, events
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d6fc8345ca90414f410dde9a089d9529ed19536b
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387575"
---
# <a name="respond-to-and-propagate-changes"></a>响应并传播更改

创建、删除或更新元素时，可以编写代码，将更改传播到模型的其他部分，或传播到外部资源（如文件、数据库或其他组件）。

## <a name="reference"></a>参考

作为一项准则，请考虑采用以下顺序的这些方法：

|方法|方案|更多信息|
|-|-|-|
|定义计算域属性。|一个域属性，其值根据模型中的其他属性计算。 例如，一个价格，它是相关元素的价格之和。|[计算的和自定义的存储属性](../modeling/calculated-and-custom-storage-properties.md)|
|定义自定义存储域属性。|存储在模型的其他部分或外部的域属性。 例如，你可以将表达式字符串分析为模型中的树。|[计算的和自定义的存储属性](../modeling/calculated-and-custom-storage-properties.md)|
|重写更改处理程序，如 OnValueChanging 和 OnDeleting|使不同的元素保持同步，使外部值与模型保持同步。<br /><br /> 将值约束到定义的范围。<br /><br /> 在属性值和其他更改之前和之后立即调用。 可以通过引发异常来终止更改。|[域属性值更改处理程序](../modeling/domain-property-value-change-handlers.md)|
|规则|可以定义在事务结束之前排队等待执行的规则，其中发生了更改。 它们不会在撤消或重做时执行。 使用它们使存储的一部分与另一部分保持同步。|[规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)|
|存储事件|建模存储提供事件通知，例如添加或删除元素或链接或更改属性的值。 事件还会在"撤消"和"重做"上执行。 使用存储事件更新不在存储中的值。|[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)|
|.NET 事件|形状具有事件处理程序，可响应鼠标单击和其他手势。 必须注册每个 对象的这些事件。 注册通常在 InitializeInstanceResources 的重写中完成，并且必须针对每个元素完成。<br /><br /> 这些事件通常在事务外部发生。|[如何：截获对形状或修饰器的单击](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)|
|边界规则|边界规则专门用于约束形状边界。|[BoundsRules 约束形状位置和大小](/previous-versions/visualstudio/visual-studio-2015/modeling/boundsrules-constrain-shape-location-and-size?preserve-view=true&view=vs-2015)|
|选择规则|选择规则专门约束用户可以选择哪些内容。|[如何：访问和约束当前所选内容](../modeling/how-to-access-and-constrain-the-current-selection.md)|
|OnAssocatedPropertyChanged|使用形状和连接线的特征（如阴影、箭头、颜色和线条宽度和样式）指示模型元素状态。|[更新形状和连接线以反映模型](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)|

## <a name="compare-rules-and-store-events"></a>比较规则和存储事件

更改通知程序、规则和事件在模型中发生更改时运行。

规则通常在发生更改的结束事务中应用，在提交事务中的更改后应用事件。

使用存储事件将模型与 Store 外部的对象同步，并使用规则在存储中保持一致性。

- **创建自定义规则** 从抽象规则创建自定义规则作为派生类。 还必须通知框架有关自定义规则。 有关详细信息，请参阅 [规则在模型中传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

- **订阅事件** 在订阅事件之前，请创建事件处理程序和委托。 然后使用 <xref:Microsoft.VisualStudio.Modeling.Store.EventManagerDirectory%2A> 属性订阅事件。 有关详细信息，请参阅事件 [处理程序在模型 外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

- **撤消更改** 撤消事务时，将引发事件，但不应用规则。 如果规则更改了值并撤消了该更改，则该值在撤消操作期间将重置为原始值。 引发事件时，必须手动将值更改回其原始值。 若要详细了解事务和撤消，请参阅 [如何：使用事务更新模型](../modeling/how-to-use-transactions-to-update-the-model.md)。

- **将事件参数传递给规则和事件** 事件和规则都传递 `EventArgs` 了一个参数，该参数包含有关模型更改方式的信息。

## <a name="see-also"></a>另请参阅

- [如何：截获对形状或修饰器的单击](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)
- [编写代码以自定义Domain-Specific语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)