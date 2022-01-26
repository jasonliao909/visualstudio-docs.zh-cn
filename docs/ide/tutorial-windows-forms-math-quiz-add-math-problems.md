---
title: 教程：向 Windows 窗体应用添加数学题
description: 了解如何使用 Visual Studio IDE 将事件处理程序和随机数学题添加到数学测验 Windows 窗体应用中。
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
ms.openlocfilehash: 6b61e41b921120c391e1b18176e076635c5d4213
ms.sourcegitcommit: 7746657b87b22a7684e79e508af598b02dfe24b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/21/2022
ms.locfileid: "137609693"
---
# <a name="tutorial-add-math-problems-to-a-math-quiz-winforms-app"></a>教程：向数学测验 WinForms 应用中添加数学题

在本系列的四个教程中，你将创建一个数学测验。 测验包含四个随机数学问题，测验者需要尝试在指定的时间内回答这些问题。

控件使用 C# 或 Visual Basic 代码。 在此第二个教程中，你将添加基于随机数的数学题的代码，从而让测验变得有挑战性。 还会创建一个名为 `StartTheQuiz()` 的方法来填充问题。

在第二个教程中，你将了解如何：

> [!div class="checklist"]
> - 编写代码以创建用于数学题的 Random 对象。
> - 为开始按钮添加事件处理程序。
> - 编写代码以开始测验。

## <a name="prerequisites"></a>先决条件

本教程基于前面的教程[创建数学测验 WinForms 应用](tutorial-windows-forms-math-quiz-create-project-add-controls.md)构建。 如果你尚未完成该教程，请先完成该教程。

## <a name="create-a-random-addition-problem"></a>创建随机加法问题

1. 在你的 Visual Studio 项目中，选择“Windows 窗体设计器”。

1. 选择窗体“Form1”。

1. 在菜单栏上，选择“视图” > “代码” 。 此时将显示 Form1.cs 或 Form1.vb（具体取决于你所使用的编程语言），以便你查看窗体背后的代码。

1. 通过在代码顶部附近添加 `new` 语句来创建一个 <xref:System.Random> 对象。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step2/cs/form1.cs" id="Snippet1":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step2/vb/form1.vb" id="Snippet1":::

   [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

   可以使用与此类似的 `new` 语句创建按钮、标签、面板、OpenFileDialogs、ColorDialogs、SoundPlayers、Randoms，甚至是窗体。 这些项称为“对象”。

   运行程序时，窗体将启动。 窗体背后的代码将创建一个 Random 对象并将其命名为“randomizer”。

   你的测验需要变量来存储其为每个问题创建的随机数字。 使用变量前，请声明这些变量，也就是列出它们的名称和数据类型。

1. 将两个整型变量添加到窗体，并将它们分别命名为“addend1”和“addend2”。

   > [!NOTE]
   > 整数变量在 C# 中表示为“int”，在 Visual Basic 中表示为“Integer” 。 这种变量可以存储从 -2147483648 到 2147483647 的正负数，并仅能存储整数而不能存储小数。

   应使用与添加 Random 对象相似的语法来添加整数变量，如下面的代码所示。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step2/cs/form1.cs" id="Snippet2":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step2/vb/form1.vb" id="Snippet2":::

1. 添加名为 `StartTheQuiz()` 的方法。 此方法使用 Random 对象的 <xref:System.Random.Next> 方法来为标签生成随机数字。 `StartTheQuiz()` 最终将填充所有问题，然后启动计时器，因此请将此信息添加到摘要注释中。 该函数应类似于以下代码。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step2/cs/form1.cs" id="Snippet3":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step2/vb/form1.vb" id="Snippet3":::

   对 Random 对象使用 `Next()` 方法时（例如，在调用 `randomizer.Next(51)` 时），将获得一个小于 51（或介于 0 和 50）的随机数。 此代码将调用 `randomizer.Next(51)`，以便两个随机数相加的答案介于 0 和 100。

   详细了解这些语句。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step2/cs/form1.cs" id="Snippet18":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step2/vb/form1.vb" id="Snippet18":::

   这些语句设置“plusLeftLabel”和“plusRightLabel”的“Text”属性，以便它们显示两个随机数。   标签控件以文本格式显示值，并且在编程中，字符串保存文本。 每个整数的 `ToString()` 方法都会将整数转换为标签可以显示的文本。

## <a name="create-random-subtraction-multiplication-and-division-problems"></a>创建随机减法、乘法和除法题

下一步是声明变量并为其他数学题提供随机值。

1. 在加法题变量后，向窗体中添加其余数学题的整数变量。 代码应类似于以下示例。

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb" range="2-27":::
   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs" range="14-38":::

1. 通过添加以下代码来修改 `StartTheQuiz()` 方法，以“Fill in the subtraction problem”注释开头。

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb" range="35-79":::
   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs" range="51-94":::

   此代码在 <xref:System.Random> 类的 <xref:System.Random.Next> 方法的使用方式上与加法题略有不同。 当您为 `Next()` 方法赋予两个值时，它会选取一个大于等于第一个值但小于第二个值的随机数。

   通过将 `Next()` 方法与两个参数一起使用，可以确保减法题的答案是正数，乘法题答案的最大值为 100，而除法题的答案不是分数。

## <a name="add-an-event-handler-to-the-start-button"></a>为开始按钮添加事件处理程序

在本部分中，你将添加代码，以便在选择“开始”按钮时开始测验。 为响应按钮选择等事件而运行的代码称为事件处理程序。

1. 在“Windows 窗体设计器”中，双击“开始测验”按钮，或选择该按钮并按 Enter 键  。 此时将显示窗体的代码，并显示新方法。

   这些操作将向“开始”按钮添加一个 Click 事件处理程序。 当测验者选择此按钮时，应用将运行你要添加到此新方法中的代码。

1. 添加以下两个语句，以使事件处理程序开始测验。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step2/cs/form1.cs" id="Snippet4":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step2/vb/form1.vb" id="Snippet4":::

   第一个语句将调用新的 `StartTheQuiz()` 方法。 第二个语句将“startButton”控件的“Enabled”属性设置为 `false`，从而使测验者在测验期间不能选择此按钮 。

## <a name="run-your-app"></a>运行应用

1. 保存代码。

1. 运行应用，然后选择“开始测验”。 随即出现随机数学题，如以下屏幕截图所示。

   :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/random-math-problems.png" alt-text="屏幕截图显示所有四个数学题中的随机值。“开始测验”按钮显示为灰色。":::

## <a name="next-steps"></a>后续步骤

前往下一教程，将计时器添加到数学测验中并检查用户答案。
> [!div class="nextstepaction"]
> [教程第 3 部分：向数学测验 WinForms 应用添加计时器控件](tutorial-windows-forms-math-quiz-add-timer.md)