---
title: 工作流设计器 - ForEach &lt; T &gt; 活动设计器
description: 了解 ForEach 活动如何针对指定 Values 集合中每个项执行 <T> 其 Body 中包含的活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ForEach`1.UI
ms.assetid: 67097b3a-fcf5-4a72-beb1-2c7784151a86
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 22ab21d25420296ba800ccecbc09257f67f8834e79813169d1e4c06a02d682dd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394025"
---
# <a name="foreachlttgt-activity-designer"></a>ForEach &lt; T &gt; 活动设计器

对于指定 <xref:System.Activities.Statements.ForEach%601> 集合中的每一项，<xref:System.Activities.Statements.ForEach%601.Body%2A> 活动执行包含在它的 <xref:System.Activities.Statements.ForEach%601.Values%2A> 中的活动。

## <a name="foreacht-properties-in-the-workflow-designer"></a>ForEach<T \> 属性工作流设计器

下表列出最有用的 <xref:System.Activities.Statements.ForEach%601> 活动属性并说明如何在设计器中使用它们。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.ForEach%601> 活动的友好名称。 默认值为 ForEach<Int32 \> 。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.ForEach%601.Values%2A>|正确|要循环访问的项的集合。 若要设置 <xref:System.Activities.Statements.ForEach%601.Values%2A> ，在 **ForEach \>** Visual Basic T活动设计器或属性网格的"值"框中<表达式。|
|*TypeArgument*|正确|由泛型参数 T 指定的 <xref:System.Activities.Statements.ForEach%601.Values%2A> 集合中的项 *的类型*。默认情况下 *，TypeArgument* 设置为 **Int32**。 若要更改类型，请更改属性网格中 *TypeArgument* 组合框的值。|

默认情况下，循环迭代器 **名为项**。 可在 <xref:System.Activities.Statements.ForEach%601> 活动设计器中更改迭代器变量的名称。 循环迭代器可在 <xref:System.Activities.Statements.ForEach%601> 活动的子级中的表达式中使用。

## <a name="see-also"></a>另请参阅

- [ParallelForEach\<T>](../workflow-designer/parallelforeach-t-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)
