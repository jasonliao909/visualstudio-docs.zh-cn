---
title: 工作流设计器 - 引发活动设计器
description: 了解 Throw 活动，以及如何使用 Throw 活动设计器创建和配置 Throw 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Throw.UI
ms.assetid: 5e97c947-be39-4a1f-af04-000e2e09528a
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 8517ac1cfc2a1a4ba0c3a1c28e17970bea6e1598
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122098965"
---
# <a name="throw-activity-designer"></a>Throw 活动设计器

**Throw** 活动设计器用于创建和配置 <xref:System.Activities.Statements.Throw> 活动。

## <a name="the-throw-activity"></a>Throw 活动

<xref:System.Activities.Statements.Throw> 活动会引发一个异常。

### <a name="using-the-throw-activity-designer"></a>使用 Throw 活动设计器

访问工具箱 的"错误 **处理"类别中** 的 **Throw** 活动 **设计器**。

可以将 **Throw** 活动设计器从"工具箱"拖动到工作流设计器放置活动的位置（例如 位于 内）上 <xref:System.Activities.Statements.Sequence> 。 这会创建默认 <xref:System.Activities.Statements.Throw> **DisplayName** 为 Throw 的活动。 可以在 Throw 活动设计器的标头或属性网格的 <xref:System.Activities.Activity.DisplayName%2A> **DisplayName** 框中编辑该值。 <xref:System.Activities.Statements.Throw.Exception%2A> 属性必须在属性网格上编辑。

### <a name="the-throw-properties"></a>Throw 属性

下表列出 <xref:System.Activities.Statements.Throw> 属性并说明如何在设计器中使用它们。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.Throw> 活动的可选友好名称。 默认值为 Throw。|
|<xref:System.Activities.Statements.Throw.Exception%2A>|正确|要引发的异常。 此异常必须派生自 <xref:System.Exception>。 若要指定此异常，请在属性网格中键入 Visual Basic 表达式。|

## <a name="see-also"></a>请参阅

- [集合](../workflow-designer/collection-activity-designers.md)
- [Rethrow](../workflow-designer/rethrow-activity-designer.md)
- [Throw 活动设计器](../workflow-designer/throw-activity-designer.md)
- [TryCatch](../workflow-designer/trycatch-activity-designer.md)
