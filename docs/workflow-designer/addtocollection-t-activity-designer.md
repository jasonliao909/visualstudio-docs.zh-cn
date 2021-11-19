---
title: AddToCollection&lt;T&gt; 活动设计器
description: 了解如何使用 AddToCollection<T> 活动设计器在工作流设计器中创建和配置 AddToCollection <T> 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.AddToCollection`1.UI
ms.assetid: f7fc0702-164e-4370-8946-bb2f9f9384b7
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: a204e6147b18938d20a94c0a41c06e8983d4026e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664687"
---
# <a name="addtocollectiont-activity-designer"></a>AddToCollection\<T> 活动设计器

AddToCollection\<T> 活动设计器用于创建和配置 <xref:System.Activities.Statements.AddToCollection%601> 活动。

## <a name="the-addtocollectiont-activity"></a>AddToCollection\<T> 活动

<xref:System.Activities.Statements.AddToCollection%601> 活动向集合添加一项。

### <a name="using-the-addtocollectiont-activity-designer"></a>使用 AddToCollection\<T> 活动设计器

可以在“工具箱”的“集合”类别（通过单击工作流设计器的“工具箱”选项卡来访问）中找到 AddToCollection\<T> 活动设计器   。 或者，从“视图”菜单中选择“工具箱”或按 Ctrl+Alt+X    。

可以将 AddToCollection\<T> 活动设计器从“工具箱”拖放到工作流设计器图面上放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内 。 放置 AddToCollection\<T> 活动设计器将创建一个 <xref:System.Activities.Statements.AddToCollection%601> 活动，其默认的 <xref:System.Activities.Activity.DisplayName%2A> 为 AddToCollection<Int32\>。 （默认情况下，TypeArgument 为 Int32。 可以在属性网格中更改 TypeArgument。可以在 AddToCollection<T\> 活动设计器的标头中或在属性网格的“DisplayName”框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值 。 其他属性必须在属性网格上编辑。

### <a name="the-addtocollectiont-properties"></a>AddToCollection\<T> 属性

下表列出 <xref:System.Activities.Statements.AddToCollection%601> 属性并说明如何在设计器中使用它们。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.AddToCollection%601> 活动的友好名称。 默认值为 AddToCollection<Int32\>。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.AddToCollection%601.Item%2A>|True|要添加到 Collection\<T> 的项。 此项的类型为 T，属于类型 TypeArgument。 若要指定项，请在属性网格中键入 Visual Basic 表达式。|
|<xref:System.Activities.Statements.AddToCollection%601.Collection%2A>|True|项应添加到的集合。 此集合的类型为 ICollection<TypeArgument\>。 若要指定集合，请在属性网格中键入 Visual Basic 表达式。|
|*TypeArgument*|True|包含在 <xref:System.Collections.Generic.ICollection%601> 中的项的类型 T。 默认情况下，此 TypeArgument 类型设置为“Int32”。 若要更改类型，请在属性网格的组合框中更改 TypeArgument 的值。|

## <a name="see-also"></a>另请参阅

- [集合](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T> 活动设计器](../workflow-designer/addtocollection-t-activity-designer.md)
- [ClearCollection\<T>](../workflow-designer/clearcollection-t-activity-designer.md)
- [ExistsInCollection\<T>](../workflow-designer/existsincollection-t-activity-designer.md)
- [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)
