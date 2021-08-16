---
title: 工作流设计器中的错误消息
description: 了解使用事件处理时可能会遇到的错误消息工作流设计器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- WFDErrorMessages.UI
- System.Activities.Presentation.ErrorActivity.UI
- System.Activities.Presentation.View.ErrorView.UI
ms.assetid: 4d8bbc2e-34fc-477f-9140-4adfd70c34a0
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 2e7bf7553867e832c03eb921e6aff51a61ab8b460b5b38fddf10ad01d78a2bf8
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121407975"
---
# <a name="error-messages-in-workflow-designer"></a>工作流设计器中的错误消息

本主题介绍使用事件处理时可能会遇到的错误消息工作流设计器。

## <a name="situations-in-which-errors-in-the-workflow-designer-occur"></a>工作流设计器中出现错误的情况

以下情况工作流设计器中出现错误：

1. 表达式中存在错误。

2. 活动的验证约束未满足。

3. XAML 文件中存在错误，导致活动无法加载。

4. XAML 文件中存在错误，导致工作流无法加载。

无效的表达式和未满足的验证约束不会导致工作流无法生成。 生成工作流成功，但 <xref:System.Activities.InvalidWorkflowException> 会运行时引发 。 如果 XAML 文件中存在错误，生成将失败。

在 Visual Studio中，加载工作流时，其错误将显示在"错误 **列表"中**。 若要导航到作为错误源的活动，请双击"错误列表 **"中的错误**。

### <a name="expression-errors"></a>表达式错误
 无效表达式用红色圆圈表示，并且该表达式旁有一个白色感叹号。 悬停在此图标上将显示描述错误来源的工具提示。 在Visual Studio，单击表达式以查看为错误源添加下划线的行。 悬停在此加下划线的文本上将显示描述错误来源的工具提示。

### <a name="activity-validation-errors"></a>活动验证错误
 活动的验证约束未满足时，红色圆圈及白色感叹号显示在该活动的右上角。 悬停在此图标上将显示描述错误来源的工具提示。

### <a name="xaml-load-errors"></a>XAML 加载错误
 当无法加载活动时，将显示一个红色框，其文本为"由于 XAML 中的错误，无法加载活动"。 当无法解析活动的类型时，通常会发生这种情况。 可以在设计器中删除无效的活动，方法是选中红色框，然后删除它。

### <a name="workflow-load-errors"></a>工作流加载错误
 当工作流无法加载时，设计器工作流设计器显示文本"遇到文档问题"，以及导致工作流加载失败的异常信息。 这通常发生在无法分析 XAML 文件时。
