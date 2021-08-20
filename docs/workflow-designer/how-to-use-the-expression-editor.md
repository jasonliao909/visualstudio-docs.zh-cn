---
title: 工作流设计器 - 如何：使用表达式编辑器
description: 了解表达式编辑器是一工作流设计器控件，可在许多工作流活动中用于输入和计算表达式。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122130450"
---
# <a name="how-to-use-the-expression-editor"></a>如何：使用表达式编辑器

表达式编辑器是一工作流设计器控件，用于许多工作流活动以输入和计算表达式。 表达式编辑器提供完整的 IDE 编辑体验，包括 IntelliSense、着色、ParamInfo、错误锯齿和其他功能。 输入表达式后，编译器将验证表达式。 如果表达式无效，则显示一个错误图标。 还可以将编辑器作为"表达式编辑器 **"对话框** 打开。

表达式是绑定到参数或属性的文本值或 Visual Basic 代码。 它们包含值元素 (例如变量、常量、文本、属性) 与操作组合以生成新值。 表达式使用 VB.NET 语法编写，即使应用程序使用 C# 编程也如此。 这意味着大写并不重要，比较是使用单个等号 ("="而不是"==") 执行的，布尔运算符是单词"and"和"or"而不是符号"&&"和"||"，并且使用 Nothing 而不是 **null**。  有关中表达式和运算符和Visual Basic，请参阅 中的运算符和[Visual Basic。](/previous-versions/visualstudio/visual-studio-2010/a1w3te48(v=vs.100))

表达式 **编辑器** 的行为如下：

- 当焦点不在表达式编辑器上时，该编辑器看上去像一个常规 TextBlock 控件。

- 当焦点在表达式编辑器上时，该编辑器的外观和行为都类似于表达式编辑器控件。 失去焦点后，表达式编辑器将再次看起来像常规 TextBlock。

- 如果在重新承载的工作流设计器中将焦点置于表达式编辑器，则该编辑器的行为类似于 TextBox。 当在重新承载的工作流设计器中失去焦点后，表达式编辑器看上去又像一个常规 TextBlock 了。

> [!NOTE]
> 表达式编辑器的 IntelliSense 仅在 Visual Studio。 在Visual Studio重新主机方案中，编译器在输入表达式后验证表达式，如果表达式无效，表达式编辑器将显示错误图标。

## <a name="use-the-expression-editor"></a>使用表达式编辑器

1. 在Visual Studio中，打开新的或现有的工作流项目。

2. 向工作流添加诸如 <xref:System.Activities.Statements.Assign> 之类的活动。

    > [!NOTE]
    > 多种工作流活动具有表达式编辑器。 表达式 TextBlock 还显示在变量设计器、自变量设计器和动态自变量设计器中。 <xref:System.Activities.Statements.Assign> 活动用作一个示例。

3. 在 <xref:System.Activities.Statements.Assign> 活动的活动设计器中单击左侧表达式编辑器。

     灰色水印 **\<To>** 字符串 和 是 **\<Enter a VB Expression>** 活动中表达式编辑器的默认文本 <xref:System.Activities.Statements.Assign> 字符串。

4. 输入表达式。 如果您输入一个字符串，请确保在该字符串两端加上引号。 如果你选择将表达式自变量绑定到一个变量，请不要使用引号。

     完成后，选择表达式编辑器外部的区域，将焦点转移到设计器的另一部分。 移动焦点会导致编译器验证表达式，如前文所述。

     输入或编辑表达式的另一种方式是单击属性网格中属性名称旁边的省略号。 选择省略号将打开 **"表达式编辑器** "作为对话框。

## <a name="see-also"></a>请参阅

- <xref:System.Activities.Presentation.View.ExpressionTextBox>
