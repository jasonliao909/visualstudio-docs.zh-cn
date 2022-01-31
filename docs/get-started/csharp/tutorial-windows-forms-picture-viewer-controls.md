---
title: 教程：向图片查看器应用程序添加控件。
description: 在此教程中，将向图片查看器应用程序添加图片框、复选框和按钮。
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.topic: tutorial
ms.date: 01/05/2022
ms.custom:
- vs-acquisition
ms.openlocfilehash: 6d5b5bf5dfc41ae1bea89430f8a7f7874e2124ca
ms.sourcegitcommit: 20f9529648e69707063dccb2b15089bf4e9bf639
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2022
ms.locfileid: "137887593"
---
# <a name="tutorial-add-ui-controls-to-the-picture-viewer-windows-forms-app-in-visual-studio"></a>教程：向 Visual Studio 中的图片查看器 Windows 窗体应用添加 UI 控件

在此系列的三个教程中，你将创建一个 Windows 窗体应用程序，用于加载和显示图片。
Visual Studio 集成设计环境 (IDE) 提供了创建应用所需的工具。
若要了解详细信息，请参阅[欢迎使用 Visual Studio IDE](../../get-started/visual-studio-ide.md)。

此程序有一个图片框、一个复选框和几个按钮，你可以用来控制应用程序。
此教程介绍如何添加这些控件。

在第二个教程中，你将了解如何：

> [!div class="checklist"]
> - 向应用程序添加控件
> - 在布局面板中添加按钮
> - 更改控件名称和位置
> - 添加对话框组件

## <a name="prerequisites"></a>先决条件

此教程基于上一教程[创建图片查看器应用程序](tutorial-windows-forms-picture-viewer-layout.md)。
如果尚未学习此教程，请先完成此教程。

## <a name="add-controls-to-your-application"></a>向应用程序添加控件
图片查看器应用程序使用 PictureBox 控件来显示图片。
它使用一个复选框和多个按钮来管理图片和背景，以及关闭应用。
你将在 Visual Studio IDE 中从“工具箱”中添加 PictureBox 和复选框。

1. 打开 Visual Studio。 图片查看器项目显示在“打开最近使用的文件”下。

1. 在 Windows 窗体设计器中，选择在前面的教程中添加的 TableLayoutPanel。
   检查 tableLayoutPanel1 是否显示在属性窗口中 。

1. 在 Visual Studio IDE 的左侧，选择“工具箱”选项卡。如果没有看到，则从菜单栏中选择“查看” > “工具箱”或者按 Ctrl+Alt+X 键     。
   在“工具箱”中，展开“公共控件”。

1. 双击“PictureBox”，将 PictureBox 控件添加到窗体。 Visual Studio IDE 会将 PictureBox 控件添加到 TableLayoutPanel 的第一个空单元格中。

1. 选择新的 PictureBox 控件以将其选中，然后选择新 PictureBox 控件上的黑色三角形以显示其任务列表。

   ![屏幕截图显示“PictureBox 任务”对话框，其中突出显示了“在父容器中停靠”。](../media/tutorial-windows-forms-picture-viewer-controls/picture-box-tasks-dialog.png)

1. 选择“在父容器中停靠”，这会将 PictureBox 的“Dock”属性设置为“填充”  。
   可以在属性窗口中查看该值。

1. 在 PictureBox 的属性窗口中，将“ColumnSpan”属性设置为“2”  。
   PictureBox 现在填充这两列。

1. 将“BorderStyle”属性设置为“Fixed3D” 。

1. 在 Windows 窗体设计器中选择“TableLayoutPanel” 。
   然后，在“工具箱”中双击“CheckBox”项，以添加新的 CheckBox 控件 。
   由于 PictureBox 占据了 TableLayoutPanel 中的前两个单元格，因此 CheckBox 控件将添加到左下方的单元格。

1. 选择“Text”属性，然后输入“拉伸” 。

    ![屏幕截图显示了名为“Stretch”的复选框控件。](../media/tutorial-windows-forms-picture-viewer-controls/checkbox-named-stretch.png)

## <a name="add-buttons-in-a-layout-panel"></a>在布局面板中添加按钮

到目前为止，控件已添加到 TableLayoutPanel 中。
以下步骤演示了如何在 TableLayoutPanel 中向新的布局面板添加四个按钮。

1. 选择窗体上的“TableLayoutPanel”。
   打开“工具箱”，选择“容器” 。
   双击“FlowLayoutPanel”，将新控件添加到 TableLayoutPanel 的最后一个单元格。

1. 将 FlowLayoutPanel 的“Dock”属性设置为“填充” 。
   可以通过选择黑色三角形，然后选择“在父容器中停靠”来设置此属性。

   <xref:System.Windows.Forms.FlowLayoutPanel> 是一个容器，它将其他控件按顺序排列在一行中。

1. 选择新的“FlowLayoutPanel”，然后打开“工具箱”并选择“公共控件” 。
   双击“按钮”项以添加一个名为“button1”的按钮控件 。

1. 再次双击“按钮”以添加其他按钮。 IDE 将调用下一个“button2”。

1. 以这种方式再添加两个按钮。
   另一种方法是选择“button2”，然后选择“编辑” > “复制”或按 Ctrl+C 键    。
   接下来，在菜单栏上，选择“编辑” > “粘贴”或按 Ctrl+V 键   。
   粘贴按钮的副本。 此时再次粘贴该副本。 请注意，IDE 会将“button3”和“button4”添加到 FlowLayoutPanel。

1. 选择第一个按钮，并将其“Text”属性设置为“显示图片” 。

1. 分别将后面三个按钮的“Text”属性设置为“清除图片”、“设置背景色”和“关闭”   。

1. 若要调整按钮的大小并进行排列，请选择“FlowLayoutPanel”。 将“FlowDirection”属性设置为“RightToLeft” 。

   这些按钮会自行与单元格的右侧对齐，并颠倒其顺序，以使“显示图片”按钮位于右侧。
   可以在 FlowLayoutPanel 周围拖动按钮，按任意顺序排列它们。

1. 选择“关闭”按钮以将其选中。 然后，要同时选择其余按钮，请在按住 Ctrl 键的同时选择它们。

1. 在属性窗口中，将“AutoSize”属性设置为“True”  。
   调整按钮大小以适应其文本。

    ![屏幕截图显示具有四个按钮的图片查看器窗体。](../media/tutorial-windows-forms-picture-viewer-controls/buttons-autosize.png)

你可以运行程序以了解控件的外观。 选择 F5 键，选择“调试” > “开始调试”，或选择“开始”按钮   。
你添加的按钮还未执行任何操作。

## <a name="change-control-names"></a>更改控件名称

窗体上有四个按钮，在 C# 中的名称分别为“button1”、“button2”、“button3”和“button4”   。
在 Visual Basic 中，任何控件名称的第一个字母都默认大写，所以这些按钮的名称为“Button1”、“Button2”、“Button3”和“Button4”   。
使用以下步骤为它们指定包含更多信息的名称。

1. 在窗体上，选择“关闭”  按钮。
   如果你仍选择了所有按钮，请按 Esc 键取消选择。

1. 在属性窗口中查找“(名称)” 。
   将名称更改为“closeButton”。

   ![带有 closeButton 名称的“属性”窗口](../media/tutorial-windows-forms-picture-viewer-controls/close-button-name-property.png)

   IDE 不接受包含空格的名称。

1. 将其他三个按钮重命名为“backgroundButton” 、 “clearButton”和“showButton” 。
   你可通过选择“属性”  窗口中的控件选择器下拉列表来验证这些名称。
   新的按钮名称将出现。

可以更改任何控件的名称，如 TableLayoutPanel 或复选框。

## <a name="add-dialog-components"></a>添加对话框组件

你的应用可以通过组件打开图片文件并选择背景色。
组件类似于控件。
使用“工具箱”向窗体添加组件。
使用属性窗口设置其属性。

与控件不同，向窗体添加组件不会添加可见项。
相反，这将提供可使用代码触发的某些行为。
例如，组件可打开“打开文件”对话框。

在此部分，你将向窗体添加 <xref:System.Windows.Forms.OpenFileDialog> 组件和 <xref:System.Windows.Forms.ColorDialog> 组件。

1. 选择 Windows 窗体设计器（“Form1.cs [Design]”） 。 然后打开“工具箱”并选择“对话框”组 。

1. 双击“OpenFileDialog”向窗体添加一个名为“openFileDialog1”的组件 。

1. 双击“ColorDialog”，添加一个名为 colorDialog1 的组件 。
   该组件在 Windows 窗体设计器的底部显示为图标。

   ![对话框组件](../media/tutorial-windows-forms-picture-viewer-controls/components-window-forms-designer.png)

1. 选择“openFileDialog1”图标并设置以下两个属性：

   - 将“Filter”属性设置为以下值：

     ```console
     JPEG Files (*.jpg)|*.jpg|PNG Files (*.png)|*.png|BMP Files (*.bmp)|*.bmp|All files (*.*)|*.*
     ```

   - 将 Title 属性设置为以下内容：“选择一个图片文件”

   “Filter”属性设置指定“选择图片”对话框显示的类型 。

## <a name="next-steps"></a>后续步骤

请继续阅读下一篇教程，了解如何向应用程序添加代码。
> [!div class="nextstepaction"]
> [教程第 3 部分：向图片查看器添加代码](tutorial-windows-forms-picture-viewer-code.md)
