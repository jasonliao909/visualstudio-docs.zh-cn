---
title: 工作流设计器-ForEach &lt; T &gt; 活动设计器
description: 了解 ForEach 活动如何 <T> 为指定值集合中的每个项执行其主体中包含的活动。
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
ms.openlocfilehash: 2f54139ddcaf214bf63292f49b9f847effed3ba5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122114740"
---
# <a name="foreachlttgt-activity-designer"></a>ForEach &lt; T &gt; 活动设计器

对于指定 <xref:System.Activities.Statements.ForEach%601> 集合中的每一项，<xref:System.Activities.Statements.ForEach%601.Body%2A> 活动执行包含在它的 <xref:System.Activities.Statements.ForEach%601.Values%2A> 中的活动。

## <a name="foreacht-properties-in-the-workflow-designer"></a>ForEach<T \> 工作流设计器中的属性

下表列出最有用的 <xref:System.Activities.Statements.ForEach%601> 活动属性并说明如何在设计器中使用它们。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.ForEach%601> 活动的友好名称。 默认值为 ForEach<Int32 \> 。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.ForEach%601.Values%2A>|正确|要循环访问的项的集合。 若要设置 <xref:System.Activities.Statements.ForEach%601.Values%2A> ，请在 **\> ForEach<T** 活动设计器或属性网格中的 "**值**" 框中键入 Visual Basic 表达式。|
|*TypeArgument*|True|<xref:System.Activities.Statements.ForEach%601.Values%2A>由泛型参数 *T* 指定的集合中的项的类型。默认情况下， *TypeArgument* 设置为 **Int32**。 若要更改类型，请在属性网格中更改 " *TypeArgument* " 组合框的值。|

默认情况下，循环迭代器为 " **项**"。 可在 <xref:System.Activities.Statements.ForEach%601> 活动设计器中更改迭代器变量的名称。 循环迭代器可在 <xref:System.Activities.Statements.ForEach%601> 活动的子级中的表达式中使用。

## <a name="see-also"></a>请参阅

- [ParallelForEach\<T>](../workflow-designer/parallelforeach-t-activity-designer.md)
- [控制流](../workflow-designer/control-flow-activity-designers.md)
