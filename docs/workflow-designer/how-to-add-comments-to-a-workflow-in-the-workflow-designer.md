---
title: 工作流设计器 - 如何：给工作流添加备注
description: 了解 .NET Framework 4.5 如何允许开发人员在设计器中将批注添加到特定类型的项（例如活动、状态和转换项）。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.Annotations.Annotation.UI
- Annotation
ms.assetid: 9aa0e8d6-8129-4438-8389-d460611581a7
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 81de5a8b27626066fb8c85b5d13da2f387bae8c9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664681"
---
# <a name="how-to-add-comments-to-a-workflow-in-the-workflow-designer"></a>如何：在工作流设计器中给工作流添加备注

为方便创建更大、更复杂的工作流，.NET Framework 4.5 允许开发人员在设计器中将批注添加到以下类型的项：

- <xref:System.Activities.Activity>

- <xref:System.Activities.Statements.State>

- <xref:System.Activities.Statements.Transition>

- 从 <xref:System.Activities.Statements.FlowNode> 中派生的类

- <xref:System.Activities.Variable>

- <xref:System.Activities.Argument>

> [!IMPORTANT]
> 批注的内容作为纯文本保存到与工作流关联的 XAML 文件，并可能被其他人读取。 将敏感信息输入批注时要谨慎。

## <a name="adding-an-annotation-to-an-activity-in-the-designer"></a>在设计器中将批注添加到活动

1. 在工作流设计器中，右键单击其中的某个项并依次选择“批注”、“添加批注”。 

1. 在提供的空白处添加批注的文本。

   该项显示批注图标。 将鼠标悬停在批注图标上会显示批注的文本。

## <a name="displaying-an-annotation-in-an-activitys-designer"></a>在活动设计器中显示批注

1. 使用活动设计器（它具有显示在活动外的批注），单击批注装饰器中的“固定”图标。

   批注显示在活动设计器中。 在下面的屏幕快照中，活动设计器中显示批注“工作流中的开始活动”。

   ![活动设计器中显示的注释](../workflow-designer/media/annotationindesigner.png)

2. 要在活动设计器外显示批注，请将鼠标悬停在活动设计器中的批注区域，然后单击“取消固定”图标

   ![活动设计器外显示的注释](../workflow-designer/media/annotationoutsidedesigner.png)

## <a name="showing-or-hiding-all-annotations"></a>显示或隐藏所有批注

1. 右键单击一个有批注的活动。 依次选择“批注”、“显示所有批注”。 

   所有批注都显示在活动设计器中。

1. 要在活动设计器外显示所有批注，请右键单击该活动，然后依次选择“批注”、“隐藏所有批注”。 

## <a name="editing-or-deleting-an-annotation-for-an-activity"></a>编辑或删除活动的批注

1. 右键单击一个有批注的活动。

1. 选择“批注”、“编辑批注”或“删除批注”。  

   打开批注以进行编辑或删除。

1. 要立即删除所有批注，请右键单击工作流设计器，然后依次选择“批注”、“删除所有批注”。 

## <a name="adding-editing-and-deleting-an-annotation-for-a-variable-or-argument"></a>添加、编辑和删除变量或参数的批注

1. 右键单击某个变量或参数，然后选择“添加批注”。

1. 输入批注的文本。 该变量或自变量会显示一个批注图标。

1. 右键单击有批注的某个变量或参数。 选择“编辑批注”。

   打开批注以进行编辑。

1. 右键单击有批注的某个变量或参数。 选择“删除批注”。

   注释将被删除。
