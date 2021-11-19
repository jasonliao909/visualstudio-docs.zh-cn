---
title: 工作流设计器 - 如何：使用表达式编辑器
description: 了解表达式编辑器如何成为可以在许多工作流活动中用于输入和计算表达式的工作流设计器控件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.View.ExpressionTextBox.UI
ms.assetid: b5f961dd-6dda-41a9-9cae-0383d479ef3d
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 9cba7dfc832eca703991b110254a60edc3bae054
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665188"
---
# <a name="how-to-use-the-expression-editor"></a>如何：使用表达式编辑器

表达式编辑器是在许多工作流活动中用于输入和计算表达式的工作流设计器控件。 表达式编辑器提供全面的 IDE 编辑体验，包括 IntelliSense、着色、ParamInfo、错误波形曲线和其他功能。 编译器在表达式输入后对它进行验证。 如果表达式无效，则显示一个错误图标。 该编辑器还能够以“表达式编辑器”对话框的形式打开。

表达式是绑定到参数或属性的文本值或 Visual Basic 代码。 它们包含与操作进行组合以生成新值的值元素（如变量、常量、文本、属性）。 表达式使用 VB.NET 语法编写，即使应用程序使用 C# 编程也如此。 这意味着不区分大小写，使用单等号（“=”）而不是（“==”）执行比较，布尔运算符使用单词“and”和“or”而不是符号“&&”和“||”，并且使用 Nothing 而不是 NULL 。 有关 Visual Basic 中的表达式和运算符的更多信息以及一些示例，请参见 [Visual Basic 中的运算符和表达式](/previous-versions/visualstudio/visual-studio-2010/a1w3te48(v=vs.100))。

“表达式编辑器”的行为如下：

- 当焦点不在表达式编辑器上时，该编辑器看上去像一个常规 TextBlock 控件。

- 当焦点在表达式编辑器上时，该编辑器的外观和行为都类似于表达式编辑器控件。 失去焦点后，表达式编辑器再次看起来像一个普通的 TextBlock。

- 如果在重新承载的工作流设计器中将焦点置于表达式编辑器，则该编辑器的行为类似于 TextBox。 当在重新承载的工作流设计器中失去焦点后，表达式编辑器看上去又像一个常规 TextBlock 了。

> [!NOTE]
> 表达式编辑器的 IntelliSense 仅在 内可用。 在 Visual Studio 和重新承载的方案中，编译器在表达式输入后对它进行验证，如果该表达式无效，则表达式编辑器将显示一个错误图标。

## <a name="use-the-expression-editor"></a>使用表达式编辑器

1. 在 Visual Studio 中，打开一个新的或现有的工作流项目。

2. 向工作流添加诸如 <xref:System.Activities.Statements.Assign> 之类的活动。

    > [!NOTE]
    > 多种工作流活动具有表达式编辑器。 表达式 TextBlock 还显示在变量设计器、自变量设计器和动态自变量设计器中。 <xref:System.Activities.Statements.Assign> 活动用作一个示例。

3. 在 <xref:System.Activities.Statements.Assign> 活动的活动设计器中单击左侧表达式编辑器。

     灰色水印字符串 \<To> 和 \<Enter a VB Expression> 是 <xref:System.Activities.Statements.Assign> 活动中的表达式编辑器的默认文本字符串 。

4. 输入表达式。 如果您输入一个字符串，请确保在该字符串两端加上引号。 如果你选择将表达式自变量绑定到一个变量，请不要使用引号。

     完成后，请选中表达式编辑器外的一个区域以便将焦点移到设计器的其他部分。 移动焦点会使编译器如前所述验证该表达式。

     输入/编辑表达式的另一个方法是在属性网格中单击属性名旁边的省略号。 选择省略号将打开以对话框形式打开“表达式编辑器”。

## <a name="see-also"></a>另请参阅

- <xref:System.Activities.Presentation.View.ExpressionTextBox>
