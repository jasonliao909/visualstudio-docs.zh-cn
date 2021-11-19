---
title: ExistsInCollection&lt;T&gt; 活动设计器
description: 了解如何在工作流设计器中使用 ExistsInCollection <T> 活动设计器创建和配置 ExistsInCollection <T> 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ExistsInCollection`1.UI
ms.assetid: 0acf9a13-caf5-4bb4-ba22-ec37d2b7267a
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 1b5110a28dd46acff895a52d0e3c05f3f53b7700
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665199"
---
# <a name="existsincollectiont-activity-designer"></a>ExistsInCollection\<T> 活动设计器

ExistsInCollection\<T> 活动设计器用于创建和配置 <xref:System.Activities.Statements.ExistsInCollection%601> 活动。

## <a name="the-existsincollectiont-activity"></a>ExistsInCollection\<T> 活动

<xref:System.Activities.Statements.ExistsInCollection%601> 活动确定特定集合中是否存在指定项。

### <a name="using-the-existsincollectiont-activity-designer"></a>使用 ExistsInCollection\<T> 活动设计器

可以在“工具箱”的“集合”类别（通过单击工作流设计器的“工具箱”选项卡来访问）中找到 ExistsInCollection\<T> 活动设计器。 或者，从“视图”菜单栏中选择“工具箱”或按 Ctrl+Alt+X。

可以将 ExistsInCollection\<T> 活动设计器从“工具箱”拖放到工作流设计器图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内。 这将创建具有 ExistsInCollection<Int32\> 的默认 <xref:System.Activities.Activity.DisplayName%2A> 的 <xref:System.Activities.Statements.ExistsInCollection%601> 活动。 （默认情况下，TypeArgument 为 Int32。 它可以在属性网格中更改。）可以在 ExistsInCollection<T\> 活动设计器的标头中或在属性网格的“DisplayName”框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值。 其他属性必须在属性网格上编辑。

### <a name="the-existsincollectiont-properties"></a>ExistsInCollection\<T> 属性

下表列出 <xref:System.Activities.Statements.ExistsInCollection%601> 属性并说明如何在设计器中使用它们：

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.ExistsInCollection%601> 活动的友好名称。 默认值为 ExistsInCollection<Int32\>。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.ExistsInCollection%601.Item%2A>|True|要在 Collection\<T> 中查找的项。 此项的类型为 T，属于类型 TypeArgument。 若要指定项，请在属性网格中键入 Visual Basic 表达式。|
|<xref:System.Activities.Statements.ExistsInCollection%601.Collection%2A>|True|要检查该项是否存在的集合。 此集合的类型为 ICollection<TypeArgument\>。 若要指定集合，请在属性网格中键入 Visual Basic 表达式。|
|TypeArgument|True|包含在 <xref:System.Collections.Generic.ICollection%601> 中的项的类型 T。 默认情况下，此 TypeArgument 类型设置为“Int32”。 若要更改类型，请在属性网格的组合框中更改 TypeArgument 的值。|
|<xref:System.Activities.Activity%601.Result%2A>|错误|一个指示集合中是否存在指定项的值。 若要指定要绑定到结果的变量，请在属性网格中键入 Visual Basic 变量。|

## <a name="see-also"></a>另请参阅

- [集合](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)
- [ClearCollection\<T>](../workflow-designer/clearcollection-t-activity-designer.md)
- [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)