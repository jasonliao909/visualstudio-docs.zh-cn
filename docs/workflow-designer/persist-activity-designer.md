---
title: 工作流设计器 - 持久化活动设计器
description: 了解 Persist 活动，以及如何使用 Persist 活动设计器创建和配置 Persist 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Persist.UI
ms.assetid: be8648dd-3eb9-4a50-8ec1-57a8be804692
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: e2cda85d209b753480f168d2e4c5a9744f6bb03f6b34de75a4bb77431f718548
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121440456"
---
# <a name="persist-activity-designer"></a>Persist 活动设计器

Persist 活动设计器用于创建和配置 <xref:System.Activities.Statements.Persist> 活动。

## <a name="the-persist-activity"></a>Persist 活动

<xref:System.Activities.Statements.Persist> 活动用于将工作流保存到磁盘中（如有可能）。 <xref:System.Activities.Statements.Persist> 活动无法在非持久性区域中执行，例如，在 <xref:System.Activities.Statements.TransactionScope> 活动中。 如果是在非 <xref:System.Activities.Statements.Persist> 持久性范围内使用活动，则运行时会引发异常。

### <a name="using-the-persist-activity-designer"></a>使用 Persist 活动设计器

可以在 **"** 工具箱"的"运行时"类别中找到"持久化"活动设计器，可通过单击"工具箱"选项卡 (或者从"视图"菜单中选择"工具箱"或CTRL+ALT+X.) 

"**持久** 化"活动设计器可以从"工具箱"拖动到工作流设计器放置活动的位置（例如，位于 内）上 <xref:System.Activities.Statements.Sequence> 。 这会创建默认 <xref:System.Activities.Statements.Persist> **DisplayName** 为 Persist 的活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在 Persist 活动设计器的标头或属性网格的 **DisplayName** 框中编辑 。

### <a name="the-persist-properties"></a>Persist 属性

下表列出 <xref:System.Activities.Statements.Persist> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中编辑，其中一些属性可以在工作流设计器编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.Persist> 活动的友好名称。 默认值为 Persist。 虽然显示名称不是绝对必需的，但最好使用显示名称。|

## <a name="see-also"></a>另请参阅

- [executionContext](../workflow-designer/runtime-activity-designers.md)
- [TerminateWorkflow](../workflow-designer/terminateworkflow-activity-designer.md)
