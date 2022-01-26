---
title: 教程：自定义 Windows 窗体应用
description: 了解如何自定义数学测验 Windows 窗体应用。 你还将使用 Visual Studio IDE 添加事件处理程序来清除值。
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
ms.openlocfilehash: 2d21a7f75c5d045dae172adf90d54c74febeef7e
ms.sourcegitcommit: 7746657b87b22a7684e79e508af598b02dfe24b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/21/2022
ms.locfileid: "137609691"
---
# <a name="tutorial-customize-a-math-quiz-winforms-app"></a>教程：自定义数学测验 WinForms 应用

在本系列的四个教程中，你将创建一个数学测验。 测验包含四个随机数学问题，测验者需要尝试在指定的时间内回答这些问题。

本教程介绍如何通过清除默认值和自定义控件的外观来强化测验。

在此最后一个教程中，你将了解如何：

> [!div class="checklist"]
> - 添加事件处理程序以清除默认的 NumericUpDown 控件值。
> - 自定义测验。

## <a name="prerequisites"></a>先决条件

本教程基于前面的教程（从[创建数学测验 WinForms 应用](tutorial-windows-forms-math-quiz-create-project-add-controls.md)开始）构建。 如果尚未完成这些教程，请先完成这些教程。

## <a name="add-event-handlers-for-the-numericupdown-controls"></a>为 NumericUpDown 控件添加事件处理程序

测验包含测验者用于输入数字的 <xref:System.Windows.Forms.NumericUpDown> 控件。 输入答案时，需要先选择默认值，或手动删除该值。 通过添加 <xref:System.Windows.Forms.Control.Enter> 事件处理程序，可以更轻松地输入答案。 当测验对象选择每个 NumericUpDown 控件中的当前值并开始输入其他值时，此代码将立即选中并清除该当前值。

1. 选择窗体上的第一个 NumericUpDown 控件。 在“属性”对话框中，选择工具栏上的“事件”图标 。

   :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/toolbar-events-icon.png" alt-text="屏幕截图显示“属性”对话框的工具栏，其中突出显示了包含闪电符号的图标。":::

   “属性”中的“事件”选项卡显示窗体中所选项的所有可响应的事件 。 在这种情况下，列出的所有事件都与 NumericUpDown 控件相关。

1. 选择“Enter”事件，输入“answer_Enter”，然后按 Enter 键  。

   :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/enter-event.png" alt-text="屏幕截图显示已选中 Enter 事件的“属性”对话框。方法框包含 answer_Enter。":::

   代码编辑器将出现并显示你为 sum NumericUpDown 控件创建的 Enter 事件处理程序。

1. 在“answer_Enter”事件处理程序的方法中，添加以下代码：

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/vb/form1.vb" id="Snippet11":::
   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/cs/form1.cs" id="Snippet11":::

   [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

   在此代码中：

   - 第一行声明该方法。 它包含名为 `sender` 的参数。 在 C# 中，该参数为 `object sender`。 在 Visual Basic 中，它为 `sender As System.Object`。 此参数引用已触发其事件的对象，即发送方。 在此示例中，发送方对象为 NumericUpDown 控件。 
   - 方法中的第一行将发送方从泛型对象强制转换或转换为 NumericUpDown 控件。 该行还将名称“answerBox”分配给 NumericUpDown 控件。 窗体上的所有 NumericUpDown 控件都将使用此方法，而不只是加法问题的控件。
   - 下一行验证 answerBox 是否已成功地强制转换为一个 NumericUpDown 控件。
   - `if` 语句中的第一行确定 NumericUpDown 控件中当前答案的长度。
   - `if` 语句中的第二行使用答案长度来选择控件中的当前值。

   当测验者选择此控件时，Visual Studio 将触发此事件。 此代码将选择当前答案。 一旦测验者开始输入其他答案，当前的答案将被清除并替换为新答案。

1. 在“Windows 窗体设计器”中，选择减法问题的 NumericUpDown 控件。

1. 在“属性”对话框的“事件”页中，找到“Enter”事件，然后从下拉列表中选择“answer_Enter”   。 这是你刚添加的事件处理程序。

1. 对乘法和除法 NumericUpDown 控件重复上述两个步骤。

## <a name="run-your-app"></a>运行应用

1. 保存并运行程序。

1. 开始测验，然后选择 NumericUpDown 控件。 系统将自动选中现有值，然后在你开始输入其他值时自动清除现有值。

   :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/existing-value-selected.png" alt-text="屏幕截图显示包含四个随机数学题的测验应用，其中已选择第一个问题的默认答案。":::

## <a name="customize-your-quiz"></a>自定义测验

在本教程的最后一部分中，你将了解一些自定义测验和扩展所学内容的方式。

### <a name="change-the-color-of-a-label"></a>更改标签的颜色

- 使用“timeLabel”控件的“BackColor”属性，使此标签在测验只剩下 5 秒时变为红色 。

  ```csharp
  timeLabel.BackColor = Color.Red;
  ```

  ```vb
  timeLabel.BackColor = Color.Red
  ```

- 当测验结束时重置颜色。

### <a name="play-a-sound-for-a-correct-answer"></a>为正确答案播放声音

当测验参加者在 <xref:System.Windows.Forms.NumericUpDown> 控件中输入正确答案时，通过播放声音来进行提示。 为实现此功能，请为每个控件的 <xref:System.Windows.Forms.NumericUpDown.ValueChanged> 事件编写事件处理程序。 每当测验者更改控件的值时，此类事件便会触发。

## <a name="next-steps"></a>后续步骤

祝贺！ 你已完成本系列教程。 你已在 Visual Studio IDE 中完成以下编程和设计任务：

- 创建了一个使用 Windows 窗体的 Visual Studio 项目
- 添加标签、按钮和 NumericUpDown 控件
- 添加计时器
- 为控件设置事件处理程序
- 编写了 C# 或 Visual Basic 代码来处理事件

继续学习另一个关于如何构建匹配游戏的教程系列。
> [!div class="nextstepaction"]
> [教程 3：创建匹配游戏](tutorial-windows-forms-create-match-game.md)