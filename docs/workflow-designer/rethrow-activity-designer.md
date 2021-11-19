---
title: 工作流设计器 - Rethrow 活动设计器
description: 了解 Rethrow 活动，以及如何使用 Rethrow 活动设计器来创建和配置 Rethrow 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Rethrow.UI
ms.assetid: 9cfa2eda-395f-4cf3-9154-83fadd4f7452
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 5508555d2e4347a96e1eaf7319270cf3f95f3177
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665903"
---
# <a name="rethrow-activity-designer"></a>Rethrow 活动设计器

Rethrow 活动设计器用于创建和配置 <xref:System.Activities.Statements.Rethrow> 活动。

## <a name="the-rethrow-activity"></a>Rethrow 活动

<xref:System.Activities.Statements.Rethrow> 活动引发先前已引发的异常。 此活动只能在 <xref:System.Activities.Statements.Catch> 活动的 <xref:System.Activities.Statements.TryCatch> 处理程序中使用。

### <a name="use-the-rethrow-activity-designer"></a>使用 ReThrow 活动设计器

访问 Rethrow 活动设计器，其位于工具箱的“错误处理”类别中  。 可以将 Rethrow 活动设计器从“工具箱”拖放到工作流设计器图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内 。 删除活动设计器将创建一个 <xref:System.Activities.Statements.Rethrow> 活动，其默认的 DisplayName 为“Throw”。 可以在 Rethrow 活动设计器的标头中或在属性网格的“DisplayName”框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值 。

### <a name="the-rethrow-properties"></a>Rethrow 属性

下表显示 <xref:System.Activities.Statements.Rethrow> 属性并说明如何在设计器中使用它们：

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|指定 <xref:System.Activities.Statements.Rethrow> 活动的可选友好名称。 默认值为 Rethrow。|

## <a name="see-also"></a>另请参阅

- [集合](../workflow-designer/collection-activity-designers.md)
- [Throw](../workflow-designer/throw-activity-designer.md)
- [TryCatch](../workflow-designer/trycatch-activity-designer.md)
