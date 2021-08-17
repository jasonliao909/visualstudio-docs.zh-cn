---
title: 工作流设计器 - 如何：使用参数设计器
description: 了解参数设计器，以及如何使用参数设计器允许数据流入和流出活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.View.ArgumentDesigner.UI
- System.Activities.Presentation.View.DesignTimeArgument.UI
ms.assetid: 64813fd5-1ea1-499a-98b4-ab2a44b7ee5e
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 52f7d9bb06d60782e67664cf648ce03a2f7437fa
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122099056"
---
# <a name="how-to-use-the-argument-designer"></a>如何：使用自变量设计器

通过参数设计器，可以轻松允许数据流入和流出活动。 通过单击设计 **画布左下** 角的"参数"按钮访问设计器。 设计器包含以表格形式显示且可以按每个列标题排序的参数列表，默认值列 **除外** 。 每个自变量都包含名称、输入/输出/输入-输出/属性方向、类型和默认表达式值（如果有）。 名称和默认的表达式值都是可编辑的文本字段，类型和方向是下拉项。 有关详细信息，请参阅变量[和参数 (.NET) 。 ](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)

## <a name="to-create-a-new-argument"></a>创建新自变量

1. 在 Visual Studio 中打开工作流或Visual Studio。

2. 单击设计画布左下角的"参数"按钮，打开参数设计器。 此时将显示参数设计器。

3. 单击标记为"创建参数 **"的空行**。 这将使用以下默认值添加新参数的新行：Name 的 argumentx，其中 x是一个初始值为 1 的整数，该整数会自动递增以创建唯一参数名称，对于 Direction为 **In，** 对于Argument 类型为 **String。** 未为默认值 **添加任何值**。 可以在工作流设计过程中随时更改这些值。

    > [!NOTE]
    > 若要删除参数，请通过单击该参数来选择该参数，然后按 **"删除"** 键。

## <a name="see-also"></a>请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
- [变量和自变量](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)
