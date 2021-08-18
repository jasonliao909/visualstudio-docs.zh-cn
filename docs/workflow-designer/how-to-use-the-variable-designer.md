---
title: 工作流设计器 - 如何：使用变量设计器
description: 了解如何使用变量设计器创建变量，以用于数据绑定方案和条件语句。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.View.DesignTimeVariable.UI
ms.assetid: 0318dfb0-bf8f-4f92-9b86-ae4c1b2161ad
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 2391694c44c5494fb9410acd7247c59e95a1b9bf
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122099030"
---
# <a name="how-to-use-the-variable-designer"></a>如何：使用变量设计器

变量设计器用于创建在数据绑定方案和条件语句中使用的变量。 通过单击设计画布左下角的"变量"按钮来访问设计器。 设计器包含以表格形式显示并可以按每个列标题排序的变量列表，"默认"列 **除外** 。 每个变量都包含名称、变量类型、作用域和默认值（如果有）。 名称和默认值是可编辑的文本字段，而类型和作用域是下拉项。 作用域是调用变量设计器时选择的活动。 如果无法在选定的范围内创建某个变量，则范围将默认为允许变量在其范围内创建的最靠近选定内容的上级活动。 有关详细信息，请参阅变量[和参数 (.NET) 。 ](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)

 在用户显式使用其中一种排序控件、关闭并重新打开变量设计器或创建另一个变量后，才会应用排序顺序。

## <a name="to-create-a-new-variable"></a>创建新变量

1. 在 Visual Studio 中打开工作流或Visual Studio。

2. 在设计画布上，选择工作流中的一个活动。

3. 单击设计画布左下角的"变量"按钮，打开变量设计器。 此时将显示变量设计器。

4. 单击标有"创建变量 **"的空行**。 这将使用以下默认值添加新变量的新行：variablex 表示 **Name，** 其中 x 是一个初始值为 1 的整数，该整数会自动递增以创建唯一变量名称 **，String** 表示变量类型，Sequence **表示****范围**。 未为"默认" **添加任何值**。 可以在工作流设计过程中随时更改这些值。

    > [!NOTE]
    > 若要删除变量，请通过单击该变量来选择该变量，然后按 **"删除"** 键。

## <a name="see-also"></a>请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
- [变量和自变量](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)
- [如何：使用自变量设计器](../workflow-designer/how-to-use-the-argument-designer.md)
