---
title: 工作流设计器 - Interop 活动设计器
description: 了解 Interop 活动设计器，以及如何使用 Interop 活动设计器创建和配置 Interop 活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Interop.UI
ms.assetid: 800a3403-ba86-41c4-8de1-c4fee9703eb1
author: jillre
ms.author: jillfra
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 785fa491d78c0286404918f01149752af2f0dc69
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126667573"
---
# <a name="interop-activity-designer"></a>Interop 活动设计器

Interop 活动设计器用于创建和配置 <xref:System.Activities.Statements.Interop> 活动。

## <a name="the-interop-activity"></a>Interop 活动

<xref:System.Activities.Statements.Interop> 活动管理从工作流中的 <xref:System.Workflow.ComponentModel.Activity?displayProperty=fullName> 派生的活动类型的执行。

### <a name="use-the-interop-activity-designer"></a>使用 Interop 活动设计器

Interop 活动设计器可在“工具箱”的“迁移”类别中找到，“工具箱”可通过单击“工具箱”选项卡（或者，从“视图” 菜单中选择“工具箱”或按 Ctrl+Alt+X）来访问。

如果项目面向 .NET Framework 4（完整版）或更高版本，则“工具箱”只显示包含 <xref:System.Activities.Statements.Interop> 活动的[迁移](../workflow-designer/migration-activity-designers.md)类别。 如有必要，可以更改项目面向的框架版本。

可以将 Interop 活动设计器从“工具箱”拖放到工作流设计器图面上通常放置活动的任意位置，如 <xref:System.Activities.Statements.Sequence> 内。 删除 Interop 活动设计器将创建一个 <xref:System.Activities.Statements.Interop> 活动，其默认的”DisplayName”为“Interop”。 可以在“Interop”活动设计器的标头中或在属性网格的“DisplayName”框中编辑 <xref:System.Activities.Activity.DisplayName%2A>。

在“Interop”活动设计器上或属性网格中，单击“ActivityType”框中的“单击浏览”文本以打开“浏览并选择 .NET 类型”对话框。 只显示工作流 3.0 或工作流 3.5 活动类型。 也就是说，只显示派生自 <xref:System.Workflow.ComponentModel.Activity> 的类型。 有关使用此框指定类型的详细信息，请参阅[浏览和选择 .NET 类型对话框](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box.md)。

### <a name="the-interop-properties"></a>Interop 属性

下表列出 <xref:System.Activities.Statements.Interop> 属性并说明如何在设计器中使用它们。 可以在属性网格中或在工作流设计器图面上编辑这些属性。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.Interop> 活动的友好名称。 默认值为 Interop。 尽管显示名称不是必需的，但建议提供一个。|
|<xref:System.Activities.Statements.Interop.ActivityType%2A>|True|指定 <xref:System.Activities.Statements.Interop> 活动包含的活动类型。 指定的此类型必须派生自 <xref:System.Workflow.ComponentModel.Activity>。|

## <a name="see-also"></a>另请参阅

- [迁移](../workflow-designer/migration-activity-designers.md)