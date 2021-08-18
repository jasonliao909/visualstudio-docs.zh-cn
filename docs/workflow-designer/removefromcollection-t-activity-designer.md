---
title: RemoveFromCollection &lt; T &gt; 活动设计器
description: 在工作流设计器中，了解如何使用 RemoveFromCollection <T> 活动设计器创建和配置 RemoveFromCollection <T> 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.RemoveFromCollection`1.UI
ms.assetid: 6617ba26-c8bc-4aed-b746-112bf490d288
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: bcf44bbb8db921307137b2d953ecbc085b666e3d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122135311"
---
# <a name="removefromcollectiont-activity-designer"></a>RemoveFromCollection\<T> 活动设计器

**\<T> RemoveFromCollection** 活动设计器用于创建和配置 <xref:System.Activities.Statements.RemoveFromCollection%601> 活动。

## <a name="the-removefromcollectiontactivity"></a>RemoveFromCollection \<T> 活动

<xref:System.Activities.Statements.RemoveFromCollection%601> 活动从特定集合中移除指定项。

### <a name="using-the-removefromcollectiont-activity-designer"></a>使用 RemoveFromCollection \<T> 活动设计器

访问"工具箱"的"集合 **"** 类别中的 **RemoveFromCollection \<T>** 活动 **设计器**。
**\<T> RemoveFromCollection** 活动设计器可以从"工具箱"拖动，并拖放到工作流设计器图面上，无论活动通常位于何处，例如位于 内 <xref:System.Activities.Statements.Sequence> 。 这会创建 <xref:System.Activities.Statements.RemoveFromCollection%601> Int32 中默认为 <xref:System.Activities.Activity.DisplayName%2A> RemoveFromCollection<的活动 \> 。 <xref:System.Activities.Activity.DisplayName%2A>可以在 T 活动设计器的 **\> RemoveFromCollection**<或在属性网格的 **DisplayName** 框中编辑该值。 其他属性必须在属性网格上编辑。

### <a name="the-removefromcollectiont-properties"></a>RemoveFromCollection<T \> 属性

下表显示了属性 <xref:System.Activities.Statements.RemoveFromCollection%601> ，并介绍了如何在设计器中使用这些属性：

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.RemoveFromCollection%601> 活动的可选友好名称。 默认值为 Int32<RemoveFromCollection。 \><br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.RemoveFromCollection%601.Item%2A>|正确|要从集合 中删除的 **项 \<T>**。 此项的类型为 *T*，类型为 *TypeArgument*。 若要指定项，请在属性网格中键入 Visual Basic 表达式。|
|<xref:System.Activities.Statements.RemoveFromCollection%601.Collection%2A>|True|应从中移除项的集合。 此集合的类型为 **ICollection<TypeArgument \> 。** 若要指定集合，请键入Visual Basic网格中的表达式。|
|*TypeArgument*|正确|包含在 <xref:System.Collections.Generic.ICollection%601> 中的项的类型 T。 默认情况下，此 *TypeArgument* 类型设置为 **Int32**。 若要更改类型，请更改属性网格中组合框中 *TypeArgument* 的值。|
|<xref:System.Activities.Activity%601.Result%2A>|错误|一个指示指定项是否已从集合中移除的值。 若要指定要绑定到结果的变量，请在属性网格中键入一个变量。|

## <a name="see-also"></a>请参阅

- [集合](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)
- [ClearCollection\<T>](../workflow-designer/clearcollection-t-activity-designer.md)
- [ExistsInCollection\<T>](../workflow-designer/existsincollection-t-activity-designer.md)