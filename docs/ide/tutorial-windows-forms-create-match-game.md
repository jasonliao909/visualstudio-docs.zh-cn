---
title: 教程：创建匹配游戏
description: 在这些教程中，你将创建一个玩家匹配图标的游戏。 首先，使用 C# 或 VB Windows 窗体在 Visual Studio 中创建一个项目并添加布局。
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.topic: tutorial
ms.date: 01/07/2022
ms.custom:
- vs-acquisition
ms.openlocfilehash: b4f4deb5dc01a98d81a518dc3d5aeb36ae780ab8
ms.sourcegitcommit: 7746657b87b22a7684e79e508af598b02dfe24b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/21/2022
ms.locfileid: "137609490"
---
# <a name="tutorial-create-a-matching-game-winforms-app"></a>教程：创建匹配游戏 WinForms 应用

在这四个教程系列中，你将构建一个匹配游戏，玩家在其中匹配隐藏的图标对。

使用这些教程了解 Visual Studio 集成设计环境 (IDE) 中的以下任务。

- 在 <xref:System.Collections.Generic.List%601> 对象中存储对象，例如图标。
- 使用 `foreach` 循环（C# 中）或 `For Each` 循环（Visual Basic 中）循环访问列表中的各项。
- 使用引用变量跟踪窗体的状态。
- 生成事件处理程序，以响应可用于多个对象的事件。
- 创建一个计时器，进行倒计时，然后在启动后立即准确触发事件。

完成后，你将拥有一个完整的游戏。

![屏幕截图显示了你创建的游戏，网格中显示了多个匹配图标。](../ide/media/tutorial-windows-forms-create-match-game/match-game-final.png)

在第一个教程中，你将了解如何：

> [!div class="checklist"]
> - 创建一个使用 Windows 窗体的 Visual Studio 项目。
> - 添加布局元素并设置其格式。
> - 添加要显示的标签并设置其格式。

## <a name="prerequisites"></a>必备条件

若要完成本教程，必须具有 Visual Studio。
请访问 [Visual Studio 下载页](https://visualstudio.microsoft.com/vs/)获取免费版本。

## <a name="create-your-windows-forms-match-game-project"></a>创建 Windows Forms 匹配游戏项目

创建匹配游戏时，第一步是创建 Windows 窗体应用项目。

::: moniker range="vs-2017"
1. 打开 Visual Studio。

1. 从菜单栏中选择“文件”>“新建”>“项目”  。

   ![屏幕截图显示“新建项目”对话框。](../ide/media/newprojectdialogcallouts.png)

1. 在“新建项目”对话框的左侧，选择“Visual C#”或“Visual Basic”，然后选择“Windows 桌面”   。

1. 在项目模板列表中，选择“Windows 窗体应用(.NET Framework)”。 将新窗体命名为“MatchingGame”，然后选择“确定”。

   > [!NOTE]
   > 如果没有看到“Windows 窗体应用(.NET Framework)”模板，请使用 Visual Studio 安装程序安装“.NET 桌面开发”工作负载。
   >
   > ![屏幕截图显示 Visual Studio 安装程序中的 .NET 桌面开发工作负载。](../ide/media/tutorial-windows-forms-create-match-game/install-dot-net-desktop-env.png)
   >
   > 有关详细信息，请参阅[安装 Visual Studio](../install/install-visual-studio.md) 页面。
::: moniker-end

::: moniker range=">=vs-2019"
1. 打开 Visual Studio。

1. 在“开始”窗口中，选择“创建新项目”。

   ![截图显示 Visual Studio 的“开始”窗口中的“创建新项目”选项。](./media/tutorial-windows-forms-create-match-game/create-new-project-dark-theme.png)

1. 在“创建新项目”窗口中，搜索“Windows 窗体”。 然后，从“所有项目类型”列表中选择“桌面” 。

1. 针对 C# 或 Visual Basic，选择“Windows 窗体应用(.NET Framework)”模板，然后选择“下一步” 。

   ![屏幕截图显示“创建新项目”对话框，其中输入了 Windows 窗体并包含 Windows 窗体应用的选项。](./media/tutorial-windows-forms-create-match-game/create-project-windows-forms.png)

   > [!NOTE]
   > 如果未看到“Windows 窗体应用(.NET Framework)”模板，则可以通过“创建新项目”窗口安装该模板。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接 。
   >
   > ![屏幕截图显示“创建新项目”对话框内“找不到所需内容”消息中的“安装更多工具和功能”链接。](./media/tutorial-windows-forms-create-match-game/install-more-tools.png)
   >
   > 接下来，在 Visual Studio 安装程序中，选择“.NET 桌面开发”。
   >
   > ![屏幕截图显示 Visual Studio 安装程序中的 .NET Core 工作负载。](../ide/media/tutorial-windows-forms-create-match-game/install-dot-net-desktop-env.png)
   >
   > 在 Visual Studio 安装程序中，选择“修改”。 系统可能会提示你保存工作内容。 接下来，选择“继续”以安装工作负载。

1. 在“配置新项目”窗口中，将项目命名为“MatchingGame”，然后选择“创建”。

::: moniker-end

Visual Studio 将为你的应用创建解决方案。
解决方案是应用所需全部项目和文件的容器。

此时，Visual Studio 在 Windows 窗体设计器中显示一个空窗体。

## <a name="create-a-layout-for-your-game"></a>为游戏创建布局

在本部分中，你将创建游戏的 4x4 网格。

1. 单击窗体以选择“Windows 窗体设计器”。 对于 C#，该选项卡显示 Form1.cs [Design]，对于 Visual Basic 则显示 Form1.vb [Design] 。 在“属性”窗口中，设置下列窗体属性。

   - 将“Text”属性从“Form1”更改为“Matching Game”  。 该文本显示在游戏窗口的顶部。
   - 设置窗体大小。 可以通过将“Size”属性设置为“550, 550”或拖动窗体的角直到在 Visual Studio IDE 底部看到正确的大小来更改它。 

1. 选择 IDE 左侧的“工具箱”标签。
   如果看不到它，请从菜单栏中选择“查看” > “工具箱”，或按 Ctrl+Alt+X”    。

1. 从工具箱中的“容器”类别拖动 <xref:System.Windows.Forms.TableLayoutPanel> 控件或双击它。
   在“属性”窗口中为面板设置以下属性。

   - 将“BackColor”属性设置为“CornflowerBlue”。
     若要设置此属性，请选择 BackColor 属性旁边的箭头。
     在“BackColor”对话框中，选择“Web”。 
     在可用颜色名称中，选择“CornflowerBlue”。

     > [!NOTE]
     > 这些颜色未按字母顺序排列，CornflowerBlue 位于列表底部附近。

   - 通过选择大的中间按钮，从下拉列表中将“Dock”属性设置为“Fill”。 
     此选项会扩展该表，使其覆盖整个窗体。
   - 将“CellBorderStyle”属性设置为“Inset”。
     此值会在游戏板上每个单元格之间提供可视边框。
   - 选择 TableLayoutPanel 右上角的三角形按钮，以显示任务菜单。
     在任务菜单上，选择“添加行”两次以添加另外两行。
     然后选择“添加列”两次以添加另外两列。
   - 在任务菜单上，选择“编辑行和列”，打开“列和行样式”窗口 。
     对于每一列，选择“百分比”选项，然后将每列的宽度设置为 25%。
   - 从窗口顶部的列表中选择“行”，然后将每行的高度设置为 25%。
   - 完成后，选择“确定”以保存更改。

TableLayoutPanel 现在是一个 4x4 网格，包含 16 个大小相等的方块单元格。
图标稍后会显示在这些行和列中。

![屏幕截图显示具有 4x4 网格的“窗体”选项卡。](../ide/media/tutorial-windows-forms-create-match-game/match-game-grid.png)

## <a name="add-and-format-labels-to-display"></a>添加要显示的标签并设置其格式

在本部分中，你将创建标签并设置其格式，以在游戏期间显示。

1. 确保在窗体编辑器中选择了该 TableLayoutPanel。
   你应该会在“属性”窗口顶部看到“tableLayoutPanel1”。 
   如果未选中，请选择窗体上的 TableLayoutPanel，或从“属性”窗口顶部的列表中选择它。

1. 像以前一样打开工具箱，然后打开“公共控件”类别。
   将 <xref:System.Windows.Forms.Label> 控件添加到 TableLayoutPanel 的左上方单元格。
   标签控件现已在 IDE 中选中。
   为其设置下列属性。

   - 将标签的“BackColor”属性设置为“CornflowerBlue” 。
   - 将“AutoSize”属性设置为“False”。
   - 将“Dock”属性设置为“Fill”。
   - 通过选择“TextAlign”属性旁的下拉按钮并选择中间按钮，将该属性设置为“MiddleCenter” 。
     此值将确保图标显示在单元格中间。
   - 选择“Font”属性。 此时会显示一个省略号 (...) 按钮。
     选择省略号，并将“Font”值设置为“Webdings”，将“Font Style”设置为“Bold”，并将“Size”设置为“48”     。
   - 将标签的“Text”属性设置为字母“c”。

   TableLayoutPanel 的左上角单元格现在包含一个在蓝色背景上居中的黑色框。

   > [!NOTE]
   > Webdings 是 Windows 操作系统附带的图标字体。
   > 在匹配游戏中，玩家匹配图标对。
   > 此字体显示要匹配的图标。
   >
   > 在“Text”属性中尝试不同的字母，而不是 c。 
   > 感叹号是一个蜘蛛，大写 N 是一只眼，逗号是一个红辣椒。

1. 选择你的 Label 控件并将其复制到 TableLayoutPanel 中的下一单元格。
   选择 Ctrl+C 键，或在菜单栏上依次选择“编辑” > “复制”。
   然后，使用 Ctrl+**V** 或“编辑” > “粘贴”进行粘贴。

   第一个 Label 的副本将显示在 TableLayoutPanel 的第二个单元格中。
   再次粘贴它，在第三个单元格中会出现另一 Label。 一直粘贴 Label 控件，直到填充完所有单元格。

此步将完成窗体的布局。

![屏幕截图显示包含 16 个黑色方块的匹配游戏窗体。](../ide/media/tutorial-windows-forms-create-match-game/match-game-grid-fill.png)

## <a name="next-steps"></a>后续步骤

继续学习下一个教程，了解如何向每个标签分配随机图标，以及向标签添加事件处理程序。
> [!div class="nextstepaction"]
> [向匹配游戏添加图标](tutorial-windows-forms-match-game-icons.md)

