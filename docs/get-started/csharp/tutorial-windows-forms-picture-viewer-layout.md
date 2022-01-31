---
title: 教程：创建“图片查看器”Windows 窗体应用
description: 了解如何在 Visual Studio IDE 中为图片查看器应用程序创建一个 C# 或 VB WinForms 项目。 你将为应用配置布局并运行该应用。
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.topic: tutorial
ms.date: 01/05/2022
ms.custom:
- vs-acquisition
ms.openlocfilehash: 3f713c01208c0dec3909aa219a190e063c1d00d1
ms.sourcegitcommit: 20f9529648e69707063dccb2b15089bf4e9bf639
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2022
ms.locfileid: "137887545"
---
# <a name="tutorial-create-a-picture-viewer-windows-forms-app-in-visual-studio"></a>教程：在 Visual Studio 中创建一个图片查看器 Windows 窗体应用

在此系列的三个教程中，你将创建一个 Windows 窗体应用程序，用于加载和显示图片。
Visual Studio 集成设计环境 (IDE) 提供了创建应用所需的工具。
若要了解详细信息，请参阅[欢迎使用 Visual Studio IDE](../visual-studio-ide.md)。

在第一个教程中，你将了解如何：

> [!div class="checklist"]
> - 创建一个使用 Windows 窗体的 Visual Studio 项目
> - 添加布局元素
> - 运行应用程序

## <a name="prerequisites"></a>先决条件

若要完成本教程，必须具有 Visual Studio。
请访问 [Visual Studio 下载页](https://visualstudio.microsoft.com/vs/)获取免费版本。

## <a name="create-your-windows-forms-project"></a>创建 Windows 窗体项目

创建图片查看器时，第一步是创建 Windows 窗体应用项目。

::: moniker range="vs-2017"
1. 打开 Visual Studio。

1. 从菜单栏中选择“文件”>“新建”>“项目”  。

     ![屏幕截图显示“新建项目”对话框。](../media/new-project-dialog-callouts.png)

1. 在“新建项目”对话框的左侧，选择“Visual C#”或“Visual Basic”，然后选择“Windows 桌面”   。

1. 在项目模板列表中，选择“Windows 窗体应用(.NET Framework)”。 将新窗体命名为“PictureViewer”，然后选择“确定”。

   > [!NOTE]
   > 如果没有看到“Windows 窗体应用(.NET Framework)”模板，请使用 Visual Studio 安装程序安装“.NET 桌面开发”工作负载。
   >
   > ![屏幕截图显示 Visual Studio 安装程序中的 .NET 桌面开发工作负载。](../media/tutorial-windows-forms-picture-viewer-layout/install-dot-net-desktop-env.png)
   >
   > 有关详细信息，请参阅[安装 Visual Studio](../../install/install-visual-studio.md) 页面。

::: moniker-end

::: moniker range="vs-2019"
1. 打开 Visual Studio。

1. 在“开始”窗口中，选择“创建新项目”。

   ![截图显示 Visual Studio 的“开始”窗口中的“创建新项目”选项。](../media/tutorial-windows-forms-picture-viewer-layout/create-new-project-dark-theme-2019.png)

1. 在“创建新项目”窗口中，搜索“Windows 窗体”。 然后，从“项目类型”列表中选择“桌面” 。

1. 针对 C# 或 Visual Basic，选择“Windows 窗体应用(.NET Framework)”模板，然后选择“下一步” 。

   ![屏幕截图显示“创建新项目”对话框，其中输入了 Windows 窗体并包含 Windows 窗体应用的选项。](../media/tutorial-windows-forms-picture-viewer-layout/create-project-windows-forms.png)

   > [!NOTE]
   > 如果未看到“Windows 窗体应用(.NET Framework)”模板，则可以通过“创建新项目”窗口安装该模板。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接 。
   >
   > ![屏幕截图显示“创建新项目”对话框内“找不到所需内容”消息中的“安装更多工具和功能”链接。](../media/tutorial-windows-forms-picture-viewer-layout/install-more-tools.png)
   >
   > 接下来，在 Visual Studio 安装程序中，选择“.NET 桌面开发”。
   >
   > ![屏幕截图显示 Visual Studio 安装程序中的 .NET Core 工作负载。](../media/tutorial-windows-forms-picture-viewer-layout/install-dot-net-desktop-env.png)
   >
   > 在 Visual Studio 安装程序中，选择“修改”。 系统可能会提示你保存工作内容。 接下来，选择“继续”以安装工作负载。

1. 在“配置新项目”窗口中，将项目命名为“PictureViewer”，然后选择“创建”。

::: moniker-end

::: moniker range=">=vs-2022"
1. 打开 Visual Studio。

1. 在“开始”窗口中，选择“创建新项目”。

   ![截图显示 Visual Studio 的“开始”窗口中的“创建新项目”选项。](../media/tutorial-windows-forms-picture-viewer-layout/create-new-project-dark-theme.png)

1. 在“创建新项目”窗口中，搜索“Windows 窗体”。 然后，从“项目类型”列表中选择“桌面” 。

1. 针对 C# 或 Visual Basic，选择“Windows 窗体应用(.NET Framework)”模板，然后选择“下一步” 。

   ![屏幕截图显示“创建新项目”对话框，其中输入了 Windows 窗体并包含 Windows 窗体应用的选项。](../media/tutorial-windows-forms-picture-viewer-layout/create-project-windows-forms.png)

   > [!NOTE]
   > 如果未看到“Windows 窗体应用(.NET Framework)”模板，则可以通过“创建新项目”窗口安装该模板。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接 。
   >
   > ![屏幕截图显示“创建新项目”对话框内“找不到所需内容”消息中的“安装更多工具和功能”链接。](../media/tutorial-windows-forms-picture-viewer-layout/install-more-tools.png)
   >
   > 接下来，在 Visual Studio 安装程序中，选择“.NET 桌面开发”。
   >
   > ![屏幕截图显示 Visual Studio 安装程序中的 .NET Core 工作负载。](../media/tutorial-windows-forms-picture-viewer-layout/install-dot-net-desktop-env.png)
   >
   > 在 Visual Studio 安装程序中，选择“修改”。 系统可能会提示你保存工作内容。 接下来，选择“继续”以安装工作负载。

1. 在“配置新项目”窗口中，将项目命名为“PictureViewer”，然后选择“创建”。

::: moniker-end

Visual Studio 将为你的应用创建解决方案。
解决方案是应用所需全部项目和文件的容器。

此时，Visual Studio 在 Windows 窗体设计器中显示一个空窗体。

## <a name="add-a-layout-element"></a>添加布局元素

图片查看应用包含一个图片框、一个复选框和四个按钮，你将在[下一个教程](tutorial-windows-forms-picture-viewer-controls.md)中添加它们。
布局元素控制其在窗体上的位置。
此部分演示如何更改窗体的标题、调整窗体大小以及添加布局元素。

1. 在项目中，选择“Windows 窗体设计器”。
   对于 C#，该选项卡显示 Form1.cs [Design]，对于 Visual Basic 则显示 Form1.vb [Design] 。

1. 选择 Form1 中的任意位置。

1. 属性窗口现在显示窗体的各个属性。
   属性窗口通常位于 Visual Studio 的右下角。
   此部分控制各种属性，例如前景色和背景色、显示在窗体顶部的标题文本以及窗体的大小。

   如果看不到“属性”，请选择“查看” > “属性窗口”  。

1. 在属性窗口中找到“Text”属性 。
   根据列表排序的方式，您可能需要向下滚动。
   输入值“图片查看器”，然后按 Enter 键。

   窗体的标题栏中现在出现文本“图片查看器”。

   > [!NOTE]
   > 可以按类别或字母顺序显示属性。
   > 使用属性窗口中的按钮来回切换。

1. 再次选择窗体。 选择窗体右下角的拖动图柄。
   该图柄是窗体右下角的一个白色小正方形。

   ![屏幕截图显示“窗体”窗口，右下角有拖动图柄。](../media/tutorial-windows-forms-picture-viewer-layout/windows-form-drag-handle.png)

   拖动手柄以调整窗体的大小，使其更宽且更高一些。
   如果查看属性窗口，你会发现“Size”属性已更改 。
   还可通过更改“Size”属性来更改窗体的大小。

1. 在 Visual Studio IDE 的左侧，选择“工具箱”选项卡。如果没有看到，则从菜单栏中选择“查看”>“工具箱”或者按 Ctrl+Alt+X 键     。

1. 选择容器旁边的小三角形符号以打开该组。

   ![屏幕截图显示“工具箱”选项卡中的“容器”组。](../media/tutorial-windows-forms-picture-viewer-layout/toolbox-container-table-layout-panel.png)

1. 双击“工具箱”中的“TableLayoutPanel” 。
   你也可以将控件从工具箱拖动到窗体上。
   TableLayoutPanel 控件将显示在窗体中。

   ![屏幕截图显示添加了 TableLayoutPanel 控件的窗体。](../media/tutorial-windows-forms-picture-viewer-layout/table-layout-format-added.png)

   > [!NOTE]
   > 添加 TableLayoutPanel 后，如果窗体中出现标题为“TableLayoutPanel 任务”的窗口，请点击窗体内的任何位置来关闭此窗口。

1. 选择“TableLayoutPanel”。
   可以通过查看属性窗口来验证选择了什么控件。

   ![屏幕截图显示出现 TableLayoutPanel 控件的属性窗口。](../media/tutorial-windows-forms-picture-viewer-layout/table-layout-panel-properties.png)

1. 选中“TableLayoutPanel”后，找到“Dock”属性，其值为“无” 。
   选择下拉箭头，然后选择“填充”，即下拉菜单中间的大按钮。

   ![截图显示已选择“填充”的属性窗口。](../media/tutorial-windows-forms-picture-viewer-layout/dock-property.png)

   “停靠”是指窗口连接另一个窗口或区域所用的一种方式。

   TableLayoutPanel 现在填充整个窗体。
   如果再次调整窗体的大小，则 TableLayoutPanel 将保持停靠状态，并自行调整大小以适合窗体。

1. 在窗体中，选择“TableLayoutPanel”。
   右上角有一个黑色的小三角形按钮。

   选择该三角形以显示控件的任务列表。

   ![屏幕截图显示 TableLayoutPanel 任务。](../media/tutorial-windows-forms-picture-viewer-layout/table-layout-panel-tasks.png)

1. 选择“编辑行和列”，以显示“列和行样式”对话框 。

1. 选择“Column1”，将其大小设置为 15%。 确保已选中“百分比”按钮。

1. 选择“Column2”并将其设置为 85%。

   ![屏幕截图显示 TableLayoutPanel 的列和行样式。](../media/tutorial-windows-forms-picture-viewer-layout/layout-column-row-styles.png)

1. 在“列和行样式”对话框顶部的“显示”中，选择“行”  。 将“Row1”设置为 90% 并将“Row2”设置为 10%。 选择“确定”，保存所做更改。 

   TableLayoutPanel 现在具有一个大的顶部行、一个小的底部行、一个小的左侧列和一个大的右侧列。

   ![屏幕截图显示 TableLayoutPanel 已调整大小的窗体。](../media/tutorial-windows-forms-picture-viewer-layout/form-layout.png)

布局已完成。

   > [!NOTE]
   > 在运行应用程序之前，请通过选择“全部保存”工具栏按钮来保存应用。
   > 或者，要保存应用，请从菜单栏中选择“文件” > “全部保存”（或按 Ctrl+Shift+S 键    ）。
   > 最佳做法是尽早且经常保存。

## <a name="run-your-app"></a>运行应用

创建 Windows 窗体应用项目时，会生成一个运行的程序。
在此阶段，图片查看器应用不会执行太多操作。
它目前只是显示了一个在标题栏中显示“图片查看器”的空窗口。

若要运行应用，请执行以下步骤。

1. 使用下列方法之一：

   - 选择 F5 键。
   - 在菜单栏上，依次选择“调试” > “开始调试” 。
   - 在工具栏上，选择“开始”按钮。

   Visual Studio 运行应用。 此时将显示标题为“图片查看器”的窗口。

   ![屏幕截图显示正在运行的 Windows 窗体应用。](../media/tutorial-windows-forms-picture-viewer-layout/run-empty-windows-forms-app.png)

   查看 Visual Studio IDE 工具栏。
   运行应用程序时，工具栏上将显示更多按钮。
   利用这些按钮，你可执行停止和启动应用之类的操作，并帮助你跟踪到任何错误。

   ![屏幕截图显示可在其中停止应用的调试工具栏。](../media/tutorial-windows-forms-picture-viewer-layout/debug-toolbar.png)

1. 使用以下其中一种方法停止应用：

   - 在工具栏上，选择“停止调试”按钮。
   - 在菜单栏上，选择“调试” > “停止调试”。
   - 在键盘上，按 Shift+F5 键 。
   - 选择“图片查看器”窗口上角的“X”按钮 。

   当你从 Visual Studio IDE 内部运行应用时，该过程称为调试。
   运行应用程序以查找和修复 bug。
   您可以执行相同的过程来运行和调试其他程序。
   要了解有关调试的详细信息，请参阅[初探调试器](../../debugger/debugger-feature-tour.md)。

## <a name="next-steps"></a>后续步骤

请继续阅读下一篇教程，了解如何向图片查看器程序添加控件。
> [!div class="nextstepaction"]
> [教程第 2 部分：向图片查看器添加控件](tutorial-windows-forms-picture-viewer-controls.md)
