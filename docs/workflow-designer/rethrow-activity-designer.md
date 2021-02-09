---
title: 工作流设计器-再次引发活动设计器
description: 了解再次引发活动，以及如何使用重新引发活动设计器来创建和配置重新引发活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Rethrow.UI
ms.assetid: 9cfa2eda-395f-4cf3-9154-83fadd4f7452
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2e3615c73583e8c5c313d23fd5f9aa6d9fcd5ff4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99847318"
---
# <a name="rethrow-activity-designer"></a>Rethrow 活动设计器

重新 **引发** 活动设计器用于创建和配置 <xref:System.Activities.Statements.Rethrow> 活动。

## <a name="the-rethrow-activity"></a>重新引发活动

<xref:System.Activities.Statements.Rethrow> 活动引发先前已引发的异常。 此活动只能在 <xref:System.Activities.Statements.Catch> 活动的 <xref:System.Activities.Statements.TryCatch> 处理程序中使用。

### <a name="use-the-rethrow-activity-designer"></a>使用重新引发活动设计器

访问 "**工具箱**" 的 "**错误处理**" 类别中的重新 **抛** 活动设计器。 重新 **引发** 活动设计器可以从 " **工具箱** " 拖放到工作流设计器图面上通常放置活动的任何位置，例如中 <xref:System.Activities.Statements.Sequence> 。 删除活动设计器将创建一个 <xref:System.Activities.Statements.Rethrow> 活动，该活动具有 Throw 的默认 **DisplayName** 。 <xref:System.Activities.Activity.DisplayName%2A>可以在重新 **引发** 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑值。

### <a name="the-rethrow-properties"></a>重新引发属性

下表显示了 <xref:System.Activities.Statements.Rethrow> 这些属性，并介绍了如何在设计器中使用这些属性：

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Rethrow> 活动的可选友好名称。 默认值为 Rethrow。|

## <a name="see-also"></a>另请参阅

- [集合](../workflow-designer/collection-activity-designers.md)
- [放弃](../workflow-designer/throw-activity-designer.md)
- [TryCatch](../workflow-designer/trycatch-activity-designer.md)
