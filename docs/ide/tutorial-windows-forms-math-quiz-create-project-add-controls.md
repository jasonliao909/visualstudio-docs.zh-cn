---
title: 教程：创建“数学测验”Windows 窗体应用
description: 了解如何为数学测验应用程序创建 C# 或 Visual Basic Windows 窗体项目。 你将使用 Visual Studio IDE 向窗体中添加 UI 控件。
ms.custom:
- vs-acquisition
ms.date: 01/20/2022
ms.topic: tutorial
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: d6e4dc6b111c6c72987d5404838695661957be1f
ms.sourcegitcommit: 7746657b87b22a7684e79e508af598b02dfe24b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/21/2022
ms.locfileid: "137609680"
---
# <a name="tutorial-create-a-math-quiz-winforms-app"></a>教程：创建数学测验 WinForms 应用

在本系列的四个教程中，你将创建一个数学测验。 测验包含四个随机数学问题，测验者需要尝试在指定的时间内回答这些问题。

Visual Studio 集成开发环境 (IDE) 提供了创建应用所需的工具。 若要详细了解此 IDE，请参阅[欢迎使用 Visual Studio IDE](../get-started/visual-studio-ide.md)。

在第一个教程中，你将了解如何：

> [!div class="checklist"]
> - 创建一个使用 Windows 窗体的 Visual Studio 项目。
> - 向窗体添加标签、按钮和其他控件。
> - 设置控件的属性。
> - 保存并运行项目。

## <a name="prerequisites"></a>先决条件

若要完成本教程，必须具有 Visual Studio。 请访问 [Visual Studio 下载页](https://visualstudio.microsoft.com/vs/)获取免费版本。

## <a name="create-your-windows-forms-project"></a>创建 Windows 窗体项目

创建数学测验时，第一步是创建 Windows 窗体应用项目。

::: moniker range="vs-2017"

1. 打开 Visual Studio。

1. 从菜单栏中选择“文件”>“新建”>“项目”  。

1. 在“新建项目”对话框的左侧，选择“Visual C#”或“Visual Basic”，然后选择“Windows 桌面”   。

1. 在项目模板列表中，选择“Windows 窗体应用(.NET Framework)”。 将新窗体命名为“MathQuiz”，然后选择“确定” 。

   > [!NOTE]
   > 如果没有看到“Windows 窗体应用(.NET Framework)”模板，请使用 Visual Studio 安装程序安装“.NET 桌面开发”工作负载 。
   >
   > :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/install-dot-net-desktop-env.png" alt-text="屏幕截图显示 Visual Studio 安装程序中的 .NET 桌面开发工作负载。":::
   >
   > 有关详细信息，请参阅[安装 Visual Studio](../install/install-visual-studio.md)。

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio。

1. 在“开始”窗口中，选择“创建新项目”。

   :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/create-new-project-dark-theme-2019.png" alt-text="屏幕截图显示 Visual Studio 的“开始”窗口中的“创建新项目”选项。":::

1. 在“创建新项目”窗口中，搜索“Windows 窗体” 。 然后，从“项目类型”列表中选择“桌面” 。

1. 针对 C# 或 Visual Basic，选择“Windows 窗体应用(.NET Framework)”模板，然后选择“下一步” 。

   :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/create-project-windows-forms.png" alt-text="屏幕截图显示“创建新项目”对话框，其中突出显示了搜索框、项目类型列表和两个模板。":::

   > [!NOTE]
   > 如果未看到“Windows 窗体应用(.NET Framework)”模板，则可以通过“创建新项目”窗口安装该模板。 在“找不到所需内容?”消息中，选择“安装更多工具和功能” 。
   >
   > :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/install-more-tools.png" alt-text="屏幕截图显示“创建新项目”对话框内“找不到所需内容”消息中的“安装更多工具和功能”链接。":::
   >
   > 接下来，在 Visual Studio 安装程序中，选择“.NET 桌面开发”。
   >
   > :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/install-dot-net-desktop-env.png" alt-text="屏幕截图显示 Visual Studio 安装程序中的 .NET 桌面开发工作负载。":::
   >
   > 在 Visual Studio 安装程序中，选择“修改”。 系统可能会提示你保存工作内容。 接下来，选择“继续”以安装工作负载。

1. 在“配置新项目”窗口中，将项目命名为“MathQuiz”，然后选择“创建”  。

::: moniker-end

::: moniker range=">=vs-2022"

1. 打开 Visual Studio。

1. 在“开始”窗口中，选择“创建新项目”。

   :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/create-new-project-dark-theme.png" alt-text="屏幕截图显示 Visual Studio 的“开始”窗口中的“创建新项目”选项。":::

1. 在“创建新项目”窗口中，搜索“Windows 窗体” 。 然后，从“项目类型”列表中选择“桌面” 。

1. 针对 C# 或 Visual Basic，选择“Windows 窗体应用(.NET Framework)”模板，然后选择“下一步” 。

   :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/create-project-windows-forms.png" alt-text="屏幕截图显示“创建新项目”对话框，其中突出显示了搜索框、项目类型列表和两个模板。":::

   > [!NOTE]
   > 如果未看到“Windows 窗体应用(.NET Framework)”模板，则可以通过“创建新项目”窗口安装该模板。 在“找不到所需内容?”消息中，选择“安装更多工具和功能” 。
   >
   > :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/install-more-tools.png" alt-text="屏幕截图显示“创建新项目”对话框内“找不到所需内容”消息中的“安装更多工具和功能”链接。":::
   >
   > 接下来，在 Visual Studio 安装程序中，选择“.NET 桌面开发”。
   >
   > :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/install-dot-net-desktop-env.png" alt-text="屏幕截图显示 Visual Studio 安装程序中的 .NET 桌面开发工作负载。":::
   >
   > 在 Visual Studio 安装程序中，选择“修改”。 系统可能会提示你保存工作内容。 接下来，选择“继续”以安装工作负载。

1. 在“配置新项目”窗口中，将项目命名为“MathQuiz”，然后选择“创建”  。

::: moniker-end

Visual Studio 将为你的应用创建解决方案。 解决方案是你的应用所需的全部项目和文件的容器。

## <a name="set-form-properties"></a>设置窗体属性

选择模板并为文件命名后，Visual Studio 会打开一个窗体。 本部分演示如何更改某些窗体属性。

1. 在项目中，选择“Windows 窗体设计器”。 对于 C#，设计器选项卡显示 Form1.cs [Design]，对于 Visual Basic 则显示 Form1.vb [Design] 。

1. 选择窗体“Form1”。

1. 属性窗口现在显示窗体的各个属性。 此窗体通常位于 Visual Studio 的右下角。 如果看不到“属性”，请选择“查看” > “属性窗口”  。

1. 在属性窗口中找到“Text”属性 。 根据列表排序的方式，您可能需要向下滚动。 对于“文本”值输入“数学测验”，然后按 Enter  。

   窗体的标题栏中现在包含文本“数学测验”。

   > [!NOTE]
   > 可以按类别或字母顺序显示属性。
   > 使用属性窗口中的按钮来回切换。

1. 将窗体大小更改为 500 像素（宽）× 400 像素（高）。

   可以通过拖动窗体的边缘或拖动图柄来调整窗体的大小，直到“属性”窗口中的“Size”值显示为适当的大小 。 拖动图柄是窗体右下角的一个白色小正方形。 还可通过更改“Size”属性的值来更改窗体的大小。

1. 将“FormBorderStyle”属性的值更改为“Fixed3D”，并将“MaximizeBox”属性设置为“False”。

     这些值用于防止测验对象改变窗体大小。

## <a name="create-the-time-remaining-box"></a>创建“剩余时间”框

数学测验的右上角包含一个框。 该框显示测验剩余的秒数。 本部分演示如何对该框使用标签。 你将在本系列后面的教程中添加倒计时计时器的代码。

1. 在 Visual Studio IDE 的左侧，选择“工具箱”选项卡。如果没有看到工具箱，则从菜单栏中选择“查看” > “工具箱”或者按 Ctrl+Alt+X 键     。

1. 选择“工具箱”中的 <xref:System.Windows.Forms.Label> 控件，然后将其拖到窗体上。

1. 在“属性”框中，为标签设置以下属性：

   - 将“(Name)”设置为 timeLabel 。
   - 将“AutoSize”更改为“False”，这样你便可以调整框的大小 。
   - 将“BorderStyle”更改为“FixedSingle”以在框的周围绘制线条 。
   - 将“Size”设置为“200, 30” 。
   - 选择“Text”属性，然后选择 Backspace 键以清除“Text”值  。
   - 选择“Font”属性旁边的加号 (+)，然后将“Size”设置为“15.75”   。

1. 将标签移动到窗体的右上角。 当出现蓝色空格线时，使用它们将控件放置在窗体上。

1. 从“工具箱”中再添加一个“标签”控件，然后将其字号设置为“15.75”。

1. 将此标签的“Text”属性设置为“剩余时间” 。

1. 移动该标签，使之整齐排列在“timeLabel”标签的左侧。

   :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/time-remaining-box.png" alt-text="屏幕截图显示“剩余时间”标签和剩余时间标签。控件在窗体的右上角相互对齐排列。":::

<!-- Original material -->

## <a name="add-controls-for-the-addition-problem"></a>添加加法题的控件

测验的第一部分是加法题。 本部分介绍如何使用标签显示该题。

1. 从“工具箱”向窗体中添加“标签”控件。

1. 在“属性”框中，为标签设置以下属性：

   - 将“Text”值设置为“?”  （问号）。
   - 将“AutoSize”设置为“False” 。
   - 将“Size”设置为“60, 50” 。
   - 将字号设置为“18”。
   - 将“TextAlign”设置为“MiddleCenter” 。
   - 将“Location”设置为“50, 75”，以便将此控件置于窗体上 。
   - 将“(Name)”设置为“plusLeftLabel” 。

1. 在窗体中，选择你创建的“plusLeftLabel”标签。 通过选择“编辑” > “复制”或按 Ctrl+C 来复制标签   。

1. 通过选择“编辑” > “粘贴”或按 Ctrl+V 三次来将标签粘贴到窗体中三次   。

1. 排列这三个新标签，使之在“plusLeftLabel”标签的右侧排成一行。

1. 将第二个标签的“Text”属性设置为 +（加号） 。

1. 将第三个标签的“(Name)”属性设置为“plusRightLabel” 。

1. 将第四个标签的“Text”属性设置为 =（等于号） 。

1. 从“工具箱”向窗体中添加 <xref:System.Windows.Forms.NumericUpDown> 控件。 稍后您将了解到有关此类控件的详细信息。

1. 在“属性”框中，为 NumericUpDown 控件设置以下属性：

   - 将字号设置为“18”。
   - 将宽度设置为 100。
   - 将“(Name)”设置为 sum 。

1. 将此“NumericUpDown”控件与加法题的各 Label 控件排成一行。

   :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/addition-problem.png" alt-text="屏幕截图显示数学测验的第一行，其中显示了标签，并且带有箭头键的控件显示为零。":::

## <a name="add-controls-for-the-subtraction-multiplication-and-division-problems"></a>添加减法、乘法和除法题的控件

接下来，向窗体中添加其他数学题的标签。

1. 复制 4 个标签控件以及你为加法问题创建的 NumericUpDown 控件。 将它们粘贴到窗体中。

1. 将新控件移动到加法控件下方并对齐。

1. 在“属性”框中，为新控件设置以下属性：

   - 将第一个问号标签的“(Name)”设置为“minusLeftLabel” 。
   - 将第二个标签的“Text”设置为 -（减号） 。
   - 将第二个问号标签的“(Name)”设置为“minusRightLabel” 。
   - 将“NumericUpDown”控件的“(Name)”设置为“difference” 。

1. 复制加法控件，并将其粘贴到窗体中两次。

1. 对于第三行：

   - 将第一个问号标签的“(Name)”设置为“timesLeftLabel” 。
   - 将第二个标签的“Text”设置为 ×（乘号） 。 你可以复制本教程中的乘号，并将其粘贴到窗体中。
   - 将第二个问号标签的“(Name)”设置为“timesRightLabel” 。
   - 将“NumericUpDown”控件的“(Name)”设置为“product” 。

1. 对于第四行：

   - 将第一个问号标签的“(Name)”设置为“dividedLeftLabel” 。
   - 将第二个标签的“Text”设置为 ÷（除号） 。 你可以复制本教程中的除号，并将其粘贴到窗体中。
   - 将第二个问号标签的“(Name)”设置为“dividedRightLabel” 。
   - 将“NumericUpDown”控件的“(Name)”设置为“quotient” 。

:::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/all-math-problems.png" alt-text="屏幕截图显示包含四行问题的数学测验，其中显示带有箭头键的标签和控件。":::

## <a name="add-a-start-button-and-set-the-tab-index-order"></a>添加“开始”按钮并设置 Tab 键索引顺序

本部分介绍如何添加“开始”按钮。 你还将指定控件的 Tab 键顺序。 此顺序决定测验者使用 Tab 键从一个控件移动到下一个控件的顺序。

1. 从“工具箱”向窗体中添加 <xref:System.Windows.Forms.Button> 控件。

1. 在“属性”框中，为按钮设置下列属性：

   - 将“(Name)”设置为“startButton” 。
   - 将“Text”设置为“开始测验” 。
   - 将字号设置为“14”。
   - 将“AutoSize”设置为“True”，这可使此按钮自动调整大小以适合文本 。
   - 将“TabIndex”设置为“0” 。 此值可使“开始”按钮成为接收焦点的第一个控件。

1. 将此按钮置于窗体底部附近的中心位置。

   :::image type="content" source="./media/tutorial-windows-forms-timed-math-quiz/math-problems-start-button.png" alt-text="屏幕截图显示包含四行问题和“开始”按钮的数学测验。":::

1. 在“属性”框中，设置每个 NumericUpDown 控件的“TabIndex”属性 ：

   - 将 sum NumericUpDown 控件的“TabIndex”设置为“1”  。
   - 将“difference”NumericUpDown 控件的“TabIndex”设置为“2”  。
   - 将“product”NumericUpDown 控件的“TabIndex”设置为“3”  。
   - 将“quotient”NumericUpDown 控件的“TabIndex”设置为“4”  。

## <a name="run-your-app"></a>运行应用

数学题尚不适用于你的测验。 但你仍可以运行应用来检查 TabIndex 值是否按预期方式工作。

1. 使用以下其中一种方法保存应用：

   - 按 Ctrl+Shift+S  。
   - 在菜单栏中，选择“文件” > “保存全部” 。
   - 在工具栏上，选择“保存全部”按钮。

1. 使用下列方法之一运行应用：

   - 按 F5 。
   - 在菜单栏上，依次选择“调试” > “开始调试” 。
   - 在工具栏上，选择“开始”按钮。

1. 按 Tab 键几次，以查看焦点如何从一个控件移动到下一个控件。

## <a name="next-steps"></a>后续步骤

前往下一教程，为数学测验添加随机数学题和事件处理程序。
> [!div class="nextstepaction"]
> [教程第2部分：向数学测验 WinForms 应用添加数学题](tutorial-windows-forms-math-quiz-add-math-problems.md)