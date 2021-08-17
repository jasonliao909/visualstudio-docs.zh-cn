---
title: 工作流设计器 TryCatch 活动设计器
description: 了解 TryCatch 活动，以及如何使用 TryCatch 活动设计器创建和配置 TryCatch 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.TryCatch.UI
- System.Activities.Statements.Catch`1.UI
ms.assetid: 02a326c2-4009-442f-b7cb-e42121fd2992
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 662bea4838b06843bc529cd41adc3e2bf33425ca
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122045757"
---
# <a name="trycatch-activity-designer"></a>TryCatch 活动设计器

" **TryCatch** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.TryCatch> 活动。

## <a name="the-trycatch-activity"></a>TryCatch 活动
 <xref:System.Activities.Statements.TryCatch>活动包含一个 <xref:System.Activities.Statements.TryCatch.Try%2A> 活动、一个 **Catch \<TException>** 和一个 <xref:System.Activities.Statements.TryCatch.Finally%2A> 活动集合。 <xref:System.Activities.Statements.Catch%601> **TException** 类型的包含 <xref:System.Activities.Statements.Catch%601.ExceptionType%2A> 和 <xref:System.Activities.Statements.Catch%601.Action%2A> 。 将它们结合使用可实现典型的基于异常的错误处理机制。 <xref:System.Activities.Statements.TryCatch> 活动尝试执行其 <xref:System.Activities.Statements.TryCatch.Try%2A> 活动。 如果 <xref:System.Activities.Statements.TryCatch.Try%2A> 活动引发任何异常，则 <xref:System.Activities.Statements.TryCatch> 活动将使用其 **Catch<TException \>** 集合来匹配该异常。 如果存在匹配项，则 <xref:System.Activities.Statements.Catch%601.Action%2A> 会执行相应 **捕获 \<TException>** 的，作为异常的错误处理逻辑。 如果 <xref:System.Activities.Statements.TryCatch.Try%2A> 节中的活动已成功完成或 <xref:System.Activities.Statements.TryCatch.Catches%2A> 中的活动已成功完成，则 <xref:System.Activities.Statements.TryCatch> 活动执行其 <xref:System.Activities.Statements.TryCatch.Finally%2A> 活动。 有关详细信息，请参阅[Windows 工作流异常](/dotnet/framework/windows-workflow-foundation/exceptions)。

### <a name="using-the-trycatch-activity-designer"></a>使用 TryCatch 活动设计器

访问 "**工具箱**" 的 "**错误处理**" 类别中的 " **TryCatch** " 活动设计器。

可以将 " **TryCatch** " 活动设计器从 " **工具箱** " 拖放到工作流设计器图面上通常放置活动的任何位置，例如中 <xref:System.Activities.Statements.Sequence> 。 这将创建具有 TryCatch 的默认 <xref:System.Activities.Statements.TryCatch> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在 " **TryCatch** " 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑值。 其他属性必须在 **TryCatch** 活动设计器的图面上进行编辑。

单击 **TryCatch** 设计器右上角的展开按钮，查看展开视图中的"Try **"、"catch" 和**" **Finally** " 框。 若要添加 catch，请在 **TryCatch** 设计器中单击 "**添加新的 catch** " 按钮。 该按钮将变为类型组合框。 选择一个异常类型，然后按 Enter 键添加该 catch。 添加 **catch** 后，catch 区域将展开，并且可以将活动拖放到捕获中，以定义捕获的执行逻辑。 请注意，在展开的 catch 区域右侧有一个文本框。 可以使用此文本框为异常变量命名。 异常变量仅可用于同一 **捕获** 中的活动。

**TryCatch** 设计器不支持编辑 **捕获**。 如果要更改异常类型，则必须删除 **Catch** 并添加一个新的。 可以通过选择并删除捕获，或在通过右键单击访问的上下文菜单上选择 "**删除**" 来删除 **捕获**。

### <a name="the-trycatch-properties"></a>TryCatch 属性

下表显示了 <xref:System.Activities.Statements.TryCatch> 这些属性，并介绍了如何在设计器中使用它们。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.TryCatch> 活动的可选友好名称。 默认值是 TryCatch。|
|<xref:System.Activities.Statements.TryCatch.Try%2A>|错误|在 <xref:System.Activities.Statements.TryCatch> 执行时首先执行的活动。|
|<xref:System.Activities.Statements.TryCatch.Catches%2A>|错误|活动引发异常时要检查的 **捕获** 元素的集合 <xref:System.Activities.Statements.TryCatch.Try%2A> 。<br /><br /> 需要在 <xref:System.Activities.Statements.TryCatch.Catches%2A> 中至少添加一个活动或在 <xref:System.Activities.Statements.TryCatch.Finally%2A> 块中添加一个活动。|
|<xref:System.Activities.Statements.TryCatch.Finally%2A>|错误|执行完 <xref:System.Activities.Statements.TryCatch.Try%2A> 以及 <xref:System.Activities.Statements.TryCatch.Catches%2A> 集合中的任何必要活动时要执行的活动。<br /><br /> 需要在 <xref:System.Activities.Statements.TryCatch.Catches%2A> 中至少添加一个活动或在 <xref:System.Activities.Statements.TryCatch.Finally%2A> 块中添加一个活动。|

## <a name="see-also"></a>请参阅

- [集合](../workflow-designer/collection-activity-designers.md)
- [Rethrow](../workflow-designer/rethrow-activity-designer.md)
- [放弃](../workflow-designer/throw-activity-designer.md)
