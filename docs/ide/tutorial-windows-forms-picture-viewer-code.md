---
title: 教程：向 Windows 窗体应用添加 UI 控件
description: 了解如何使用 Visual Studio 向图片查看器 WinForms 应用添加 UI 控件。 控件是指图片框、复选框和按钮。
dev_langs:
- CSharp
- VB
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.topic: tutorial
ms.date: 01/05/2022
ms.custom:
- vs-acquisition
ms.openlocfilehash: 9d93ba0e8a6c77ddc6b90fffadea7e4243490882
ms.sourcegitcommit: 7d319435c35075d4cec021b7b667666a81c02435
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2022
ms.locfileid: "137650443"
---
# <a name="tutorial-add-code-to-the-picture-viewer-windows-forms-app-in-visual-studio"></a>教程：向 Visual Studio 中的图片查看器 Windows 窗体应用添加代码

在此系列的三个教程中，你将创建一个 Windows 窗体应用程序，用于加载和显示图片。
Visual Studio 集成设计环境 (IDE) 提供了创建应用所需的工具。
若要了解详细信息，请参阅[欢迎使用 Visual Studio IDE](../get-started/visual-studio-ide.md)。

控件使用 C# 或 Visual Basic 代码执行与其相关的操作。

在第三个教程中，你将了解如何：

> [!div class="checklist"]
> - 为控件添加事件处理程序
> - 编写代码以打开对话框
> - 为其他控件编写代码
> - 运行应用程序

## <a name="prerequisites"></a>先决条件

此教程基于前面的教程[创建图片查看器应用程序](tutorial-windows-forms-picture-viewer-layout.md)和[向图片查看器添加 UI 控件](tutorial-windows-forms-picture-viewer-controls.md)。
如果尚未学习这些教程，请先完成这些教程。

## <a name="add-event-handlers-for-your-controls"></a>为控件添加事件处理程序

在此部分，为第二个教程[向图片查看器应用程序添加控件](tutorial-windows-forms-picture-viewer-code.md)中添加的控件添加事件处理程序。
发生操作（如选择按钮）时，应用程序会调用事件处理程序。 

1. 打开 Visual Studio。 图片查看器项目显示在“打开最近使用的文件”下。

1. 在 Windows 窗体设计器中，并双击“显示图片”按钮 。
   或者，可以选择窗体上的“显示图片”按钮，然后按 Enter 键 。

   Visual Studio IDE 会在主窗口中打开一个选项卡。 在 C# 中，选项卡名为 Form1.cs。 如果使用的是 Visual Basic，则该选项卡名为 Form1.vb。

   此选项卡显示窗体后面的代码文件。

   ![屏幕截图显示了包含 Visual C# 代码的 Form1.cs 选项卡。](../ide/media/tutorial-windows-forms-picture-viewer-code/show-picture-button-code.png)

   > [!NOTE]
   > Form1.vb 选项卡可能会将“showButton”显示为“ShowButton” 。

1. 重点考虑这一部分的代码。

   ```csharp
   private void ShowButton_Click(object sender, EventArgs e)
   {
   }
   ```

   ```vb
   Private Sub showButton_Click() Handles showButton.Click

   End Sub
   ```

   [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

1. 再次选择“Windows 窗体设计器”选项卡，然后双击“清除图片”按钮以打开其代码 。
   对于剩余两个按钮，重复此操作。
   Visual Studio IDE 每次都会向窗体的代码文件添加一个新方法。

1. 双击 Windows 窗体设计器中的 CheckBox 控件以添加 `checkBox1_CheckedChanged()` 方法 。 
   选中或清除复选框时，它将调用此方法。

   下面代码片段显示了你在代码编辑器中看到的新代码。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial1step6/cs/form1.cs" id="Snippet2":::

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial1step6/vb/form1.vb" id="Snippet2":::

方法（包括事件处理程序）可以根据你的需要命名。
使用 IDE 添加事件处理程序时，IDE 将基于控件的名称和正在处理的事件创建一个名称。

例如，名为 showButton 的按钮的 Click 事件称为 `showButton_Click()` 或 `ShowButton_Click()`。 如果要更改代码的变量名，请右键单击代码中的变量，然后选择“重构” > “重命名” 。 将重命名代码中变量的所有实例。 有关更多信息，请参阅[重命名重构](../ide/reference/rename.md)。

## <a name="write-code-to-open-a-dialog-box"></a>编写代码以打开对话框

“显示图片”按钮使用 OpenFileDialog 组件显示图片文件。
此过程添加用于调用该组件的代码。

Visual Studio IDE 提供了一个名为 IntelliSense 的强大工具。
当你在键入时，IntelliSense 会建议可能的代码。

1. 在 Windows 窗体设计器中，并双击“显示图片”按钮 。 
   IDE 将光标移到 `showButton_Click()` 或 `ShowButton_Click()` 方法内。

1. 在两个大括号 `{ }` 之间或 `Private Sub...` 和 `End Sub` 之间的空行上键入一个 i。
   这时会打开一个 IntelliSense 窗口。

   ![屏幕截图显示了包含 Visual C# 代码的 IntelliSense。](../ide/media/tutorial-windows-forms-picture-viewer-code/intellisense-window.png)

1. “IntelliSense”窗口应该会突出显示 `if` 一词。 选择 Tab 键以插入 `if`。

1. 选择“true”，然后针对 C# 键入 `op` 以进行覆盖，或者针对 Visual Basic 键入 `Op` 以进行覆盖。

   ![屏幕截图显示了“显示”按钮的事件处理程序，并选择了值“true”。](../ide/media/tutorial-windows-forms-picture-viewer-code/show-button-handler-true-selected.png)

   IntelliSense 显示 openFileDialog1。

1. 选择 Tab 键以添加 openFileDialog1。 

1. 在 openFileDialog1 后直接键入句点 (`.`) 或点号。
   IntelliSense 提供 OpenFileDialog 组件的所有属性和方法。
   开始键入 `ShowDialog` 并选择 Tab 键。`ShowDialog()` 方法将显示“打开文件”对话框 。

1. 在 `ShowDialog` 中的“g”后立即添加括号：`()`。
   代码应该为 `openFileDialog1.ShowDialog()`。

1. 对于 C#，添加一个空格，然后添加两个等于号 (`==`)。 对于 Visual Basic，添加一个空格，然后使用单个等号 (`=`)。

1. 添加另一个空格。 使用 IntelliSense 输入 DialogResult。

1. 键入一个点，在 IntelliSense 窗口中打开 DialogResult 值。 输入字母 `O`，然后选择 Tab 键插入“OK”。

   > [!NOTE]
   > 第一行代码应会完成。 对于 C#，输出应如下所示。
   >
   >  `if (openFileDialog1.ShowDialog() == DialogResult.OK)`
   >
   >  对于 Visual Basic，此代码行应如下所示。
   >
   >  `If OpenFileDialog1.ShowDialog() = DialogResult.OK Then`

1. 添加以下代码行。

   ```csharp
   pictureBox1.Load(openFileDialog1.FileName);  
   ```

   ```vb
   PictureBox1.Load(OpenFileDialog1.FileName)
   ```

   可以复制并粘贴或使用 IntelliSense 添加这些代码行。
   最终的 `showButton_Click()` 方法应与以下代码类似。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial1step8/cs/form1.cs" id="Snippet1":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial1step8/vb/form1.vb" id="Snippet1":::

1. 将下面的注释添加到代码中。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial1step9_10/cs/form1.cs" id="Snippet1":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial1step9_10/vb/form1.vb" id="Snippet1":::

   最佳做法是始终注释代码。
   通过代码注释，可以在将来更轻松地理解和维护代码。

## <a name="write-code-for-the-other-controls"></a>为其他控件编写代码
如果现在运行应用程序，可以选择“显示图片”。
图片查看器将打开“打开文件”对话框，你可在其中选择要显示的图片。

在此部分，为其他事件处理程序添加代码。

1. 在 Windows 窗体设计器中，并双击“清除图片”按钮 。
   在大括号中添加代码。

   ```csharp
   private void clearButton_Click(object sender, EventArgs e)
   {
       // Clear the picture.
       pictureBox1.Image = null;
   }
   ```

   ```vb
   Private Sub clearButton_Click() Handles clearButton.Click
       ' Clear the picture.
       PictureBox1.Image = Nothing
   End Sub   
   ```

1. 双击“设置背景色”按钮，并在大括号中添加代码。

   ```csharp
   private void backgroundButton_Click(object sender, EventArgs e)
   {
       // Show the color dialog box. If the user clicks OK, change the
       // PictureBox control's background to the color the user chose.
       if (colorDialog1.ShowDialog() == DialogResult.OK)
           pictureBox1.BackColor = colorDialog1.Color;
   }
   ```

   ```vb
   Private Sub backgroundButton_Click() Handles backgroundButton.Click
       ' Show the color dialog box. If the user clicks OK, change the
       ' PictureBox control's background to the color the user chose.
       If ColorDialog1.ShowDialog() = DialogResult.OK Then
           PictureBox1.BackColor = ColorDialog1.Color
       End If
   End Sub
   ```

1. 双击“关闭”按钮，并在大括号中添加代码。

   ```csharp
   private void closeButton_Click(object sender, EventArgs e)
   {
       // Close the form.
       this.Close();
   }

   ```

   ```vb
   Private Sub closeButton_Click() Handles closeButton.Click
       ' Close the form.
       Close()
   End Sub  
   ```

1. 双击“拉伸”复选框，并在大括号中添加代码。

   ```csharp
   private void checkBox1_CheckedChanged(object sender, EventArgs e)
   {
       // If the user selects the Stretch check box, 
       // change the PictureBox's
       // SizeMode property to "Stretch". If the user clears 
       // the check box, change it to "Normal".
       if (checkBox1.Checked)
           pictureBox1.SizeMode = PictureBoxSizeMode.StretchImage;
       else
           pictureBox1.SizeMode = PictureBoxSizeMode.Normal;
   }
   ```

   ```vb
   Private Sub CheckBox1_CheckedChanged() Handles CheckBox1.CheckedChanged
       ' If the user selects the Stretch check box, change 
       ' the PictureBox's SizeMode property to "Stretch". If the user 
       ' clears the check box, change it to "Normal".
       If CheckBox1.Checked Then
           PictureBox1.SizeMode = PictureBoxSizeMode.StretchImage
       Else
           PictureBox1.SizeMode = PictureBoxSizeMode.Normal
       End If
   End Sub   
   ```

## <a name="run-your-application"></a>运行应用程序

编写应用程序时，你随时都可以运行该应用程序。
在前面部分添加代码后，图片查看器将完成。
与前面的教程一样，使用以下方法之一运行应用程序：

- 选择 F5 键。
- 在菜单栏上，依次选择“调试” > “开始调试” 。
- 在工具栏上，选择“开始”按钮。

此时将显示标题为“图片查看器”的窗口。
测试所有控件。

1. 选择“设置背景色”按钮。 随即打开“颜色”对话框。

   ![屏幕截图显示“颜色”对话框。](../ide/media/tutorial-windows-forms-picture-viewer-code/color-dialog-box.png)

1. 选择一种颜色来设置背景色。

1. 选择“显示图片”以显示图片。

   ![屏幕截图显示了显示图片的图片查看器应用。](../ide/media/tutorial-windows-forms-picture-viewer-code/run-picture-viewer.png)

1. 选择“拉伸”，然后取消选择。

1. 选择“清除图片”按钮以确保显示内容消失。

1. 选择“关闭”以退出应用。

## <a name="next-steps"></a>后续步骤

祝贺！
你已完成该系列教程。
你已在 Visual Studio IDE 中完成以下编程和设计任务：

- 创建了一个使用 Windows 窗体的 Visual Studio 项目
- 完成了图片查看应用程序的布局
- 添加了按钮和复选框
- 添加了对话框
- 为控件添加了事件处理程序
- 编写了 C# 或 Visual Basic 代码来处理事件

继续学习另一个教程系列，了解如何创建计时数学测验。
> [!div class="nextstepaction"]
> [教程 2：创建计时数学测验](tutorial-windows-forms-math-quiz-create-project-add-controls.md)
