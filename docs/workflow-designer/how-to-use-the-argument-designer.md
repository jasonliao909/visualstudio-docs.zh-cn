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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665190"
---
# <a name="how-to-use-the-argument-designer"></a>如何：使用自变量设计器

参数设计器使数据易于流入和流出活动。 单击设计画布左下角的“参数”按钮可访问设计器。 该设计器包含一个参数列表，这些参数显示在表格窗体中并可按每一列标题排序，但“默认值”列除外。 每个自变量都包含名称、输入/输出/输入-输出/属性方向、类型和默认表达式值（如果有）。 名称和默认的表达式值都是可编辑的文本字段，类型和方向是下拉项。 有关详细信息，请参阅[变量和参数 (.NET)](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)。

## <a name="to-create-a-new-argument"></a>创建新自变量

1. 在 Visual Studio 中打开一个工作流或活动解决方案。

2. 通过单击设计画布左下角的“参数”按钮打开参数设计器。 此时将显示参数设计器。

3. 单击标记为“创建参数”的空行。 这会使用以下默认值添加一个具有新参数的新行：“名称”为 argumentx，其中 x 是一个整数，该整数的初始值为 1 并自动递增，从而创建唯一的参数名称，“方向”为“输入”并且“参数类型”为“String”    。 “默认值”未添加值。 可以在工作流设计过程中随时更改这些值。

    > [!NOTE]
    > 若要删除某个参数，请单击选择该参数，然后按 Delete 键。

## <a name="see-also"></a>另请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
- [变量和自变量](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)
