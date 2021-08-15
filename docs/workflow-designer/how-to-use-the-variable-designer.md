---
title: 工作流设计器-如何：使用变量设计器
description: 了解如何使用变量设计器创建在数据绑定方案和条件语句中使用的变量。
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
ms.openlocfilehash: 84e34fbc89cdae70a100e802a3e97773330bde1f98a30c4d1e26c4012cdfab68
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121440508"
---
# <a name="how-to-use-the-variable-designer"></a>如何：使用变量设计器

变量设计器用于创建在数据绑定方案和条件语句中使用的变量。 通过单击设计画布左下角的 " **变量** " 按钮可访问该设计器。 设计器包含一个变量列表，该列表显示在表格窗体中并可按每个列标题进行排序（ **默认** 列除外）。 每个变量都包含名称、变量类型、作用域和默认值（如果有）。 名称和默认值是可编辑的文本字段，而类型和作用域是下拉项。 作用域是调用变量设计器时选择的活动。 如果无法在选定的范围内创建某个变量，则范围将默认为允许变量在其范围内创建的最靠近选定内容的上级活动。 有关详细信息，请参阅 [.net)  ( 的变量和参数 ](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)。

 在用户显式使用其中一种排序控件、关闭并重新打开变量设计器或创建另一个变量后，才会应用排序顺序。

## <a name="to-create-a-new-variable"></a>创建新变量

1. 在 Visual Studio 中打开工作流或活动解决方案。

2. 在设计画布上，选择工作流中的一个活动。

3. 通过单击设计画布左下角的 " **变量** " 按钮打开变量设计器。 此时将显示变量设计器。

4. 单击标记为 " **创建变量**" 的空行。 这会使用以下默认值添加一个具有新变量的新行： variablex 作为 **名称**，其中 x 是一个整数，其初始值为1，其初始值为1，该值将自动递增，以创建唯一的变量名称、**变量类型** 的 **字符串** 和 **作用域** 的 **序列**。 不会添加 **默认** 值。 可以在工作流设计过程中随时更改这些值。

    > [!NOTE]
    > 若要删除某个变量，请单击该变量，然后按 **delete** 键。

## <a name="see-also"></a>另请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
- [变量和自变量](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)
- [如何：使用自变量设计器](../workflow-designer/how-to-use-the-argument-designer.md)
