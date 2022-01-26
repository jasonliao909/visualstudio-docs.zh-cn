---
title: 教程：向 Windows 窗体应用添加计时器
description: 了解如何使用 Visual Studio IDE 数学测验 Windows 向窗体应用中添加计时器控件和事件处理程序。
ms.custom:
- vs-acquisition
dev_langs:
- CSharp
- VB
ms.date: 01/20/2022
ms.topic: tutorial
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 0374a72def5bfaa8edd308c2d6866ed1ce318bd6
ms.sourcegitcommit: 7746657b87b22a7684e79e508af598b02dfe24b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/21/2022
ms.locfileid: "137609697"
---
# <a name="tutorial-add-a-timer-control-to-a-math-quiz-winforms-app"></a>教程：向数学测验 WinForms 应用添加计时器控件

在本系列的四个教程中，你将创建一个数学测验。 测验包含四个随机数学问题，测验者需要尝试在指定的时间内回答这些问题。

测验使用计时器控件。 此控件背后的代码跟踪运行时间，并检查测验者的答案。

在第三个教程中，你将了解如何：

> [!div class="checklist"]
> - 添加计时器控件。
> - 为计时器添加事件处理程序。
> - 编写代码以检查用户的答案、显示消息并填写正确的答案。

## <a name="prerequisites"></a>先决条件

本教程基于前面的教程（从[创建数学测验 WinForms 应用](tutorial-windows-forms-math-quiz-create-project-add-controls.md)开始）构建。 如果尚未完成这些教程，请先完成这些教程。

## <a name="add-a-countdown-timer"></a>添加倒计时计时器

若要在测验期间持续跟踪时间，请使用计时器组件。 还需要一个变量来存储剩余的时间量。

1. 添加名为“timeLeft”的整数变量，其方式与在之前的教程中声明变量的方式相同。 将“timeLeft”声明放在紧靠在其他声明之后的位置。 代码应类似于以下示例。

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb" id="Snippet15":::
   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs" id="Snippet15":::

   [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

1. 在“Windows 窗体设计器”中，将“工具箱”的“组件”类别中的 <xref:System.Windows.Forms.Timer> 控件移到窗体中  。 此控件显示在设计窗口底部的灰色区域内。

1. 在窗体中，请选择刚才添加的“timer1”图标，并将其“Interval”属性设置为“1000”。   由于此间隔以毫秒为单位，因此值为 1000 时会导致计时器每秒引发一个 <xref:System.Windows.Forms.Timer.Tick> 事件。

## <a name="check-the-answers"></a>检查答案

由于计时器每秒引发一个 Tick 事件，所以在 Tick 事件处理程序中应该检查运行时间。 在该事件处理程序中检查答案也是可行的。 如果时间已用完，或者答案正确，则测验应结束。

在编写该事件处理程序之前，请添加一个调用 `CheckTheAnswer()` 的方法，用于确定数学题的答案是否正确。 此方法应与其他方法（如 `StartTheQuiz()`）保持一致。 代码应类似于以下示例。

:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb" id="Snippet17":::
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs" id="Snippet17":::

此方法确定数学题的答案，并将结果与 <xref:System.Windows.Forms.NumericUpDown> 控件中的值进行比较。 在此代码中：

- Visual Basic 版本使用 `Function` 关键字而不是一般的 `Sub` 关键字，因为此方法将返回一个值。

- 由于使用键盘无法方便地输入乘号 (×) 和除号 (÷)，因此 C# 和 Visual Basic 接受用星号 (*) 代替乘号，用斜线 (/) 代替除号。

- 在 C# 中，`&&` 是 `logical and` 运算符。 在 Visual Basic 中，等效的运算符是 `AndAlso`。 使用 `logical and` 运算符检查多个条件是否为 true。 在这种情况下，如果值都正确，则方法返回值 `true`。 否则，此方法将返回值 `false`。

- `if` 语句使用 NumericUpDown 控件的 Value 属性访问控件的当前值。 下一部分使用相同的属性在每个控件中显示正确答案。

## <a name="add-an-event-handler-to-the-timer"></a>向计时器添加事件处理程序

现已具有检查答案的方法，接下来可以编写 Tick 事件处理程序的代码。 在计时器引发 Tick 事件后，此代码每秒运行一次。 此事件处理程序通过调用 `CheckTheAnswer()` 来检查测验者的答案。 它还检查测验已消耗的时间。

1. 在窗体中，双击“计时器”控件，或将其选中，然后选择 Enter 键 。 这些操作将向计时器添加 Tick 事件处理程序。 代码编辑器将出现并显示 Tick 处理程序的方法。

1. 将下面的语句添加到新事件处理程序方法。

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb" id="Snippet6":::
   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs" id="Snippet6":::

   在测验中的每一秒，此方法都将运行。 代码首先检查 `CheckTheAnswer()` 返回的值。

   - 如果所有答案都正确，该值为 `true`，且测验结束：

     - 计时器停止。
     - 随即出现一条祝贺消息。
     - startButton 控件的“Enabled”属性将设置为 `true`，以便测验者可以开始其他测试 。

   - 如果 `CheckTheAnswer()` 返回 `false`，代码将检查 timeLeft 的值：

     - 如果此变量大于 0，计时器将从 timeLeft 中减去 1。 它还将更新“timeLabel”控件的“Text”属性，以便向测验者显示剩余的秒数 。
     - 如果没有剩余时间，计时器将停止并更改 timeLabel 控件的文本，使之显示“时间到!”  一个消息框宣布测验结束，并显示答案。 “开始”按钮将再次可用。

## <a name="start-the-timer"></a>启动计时器

若要在测验开始时启动计时器，请向 `StartTheQuiz()` 方法的末尾添加三行，如以下示例所示。

:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb" id="Snippet7":::
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs" id="Snippet7":::

当测验开始时，此代码将“timeLeft”变量将设置为 30，而 timeLabel 控件的“Text”属性将为 30 秒  。 然后，Timer 控件的 <xref:System.Windows.Forms.Timer.Start> 方法将开始倒计时。

## <a name="run-your-app"></a>运行应用

1. 保存并运行程序。

1. 选择“开始测验”。 计时器将开始倒计时。 当时间用完时，测验将结束，并显示答案。 

1. 开始另一个测验，并提供数学题的正确答案。 在时间限制内回答正确时，将出现一个消息框、开始按钮变为可用并且计时器停止。

   :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/quiz-end.png" alt-text="屏幕截图显示已完成测验，剩余 19 秒。“开始测验”按钮可用。":::

## <a name="next-steps"></a>后续步骤

请继续学习下一教程，了解如何自定义数学测验。
> [!div class="nextstepaction"]
> [教程第 4 部分：自定义数学测验 WinForms 应用](tutorial-windows-forms-math-quiz-customize-ui.md)