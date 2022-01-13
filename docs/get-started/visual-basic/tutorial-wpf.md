---
title: 教程：使用 Windows Presentation Foundation 创建Visual Basic
description: 在本教程中，使用 Windows WPF) UI 框架在 Visual Basic Visual Studio 创建 Windows Presentation Foundation (桌面 .NET 应用。
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.workload:
- dotnet
dev_langs:
- VB
ms.date: 01/07/2022
ms.custom: vs-acquisition, get-started
ms.openlocfilehash: b9382d659f5b90d957ff63307c050c6be219ecfb
ms.sourcegitcommit: 9b1c1cceab4c59f0b91e19ae46a51969f72fcc34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2022
ms.locfileid: "136801367"
---
# <a name="tutorial-create-a-wpf-application-with-visual-basic"></a>教程：使用应用程序创建 WPF Visual Basic

在本教程中，你将使用 IDE Visual Basic集成Visual Studio环境中 (应用程序) 。
程序将使用 WPF Windows Presentation Foundation (UI 框架) WPF。
使用本教程可以熟悉许多可在其中使用的工具、对话框和Visual Studio。

在本教程中，你将了解如何执行以下操作：

> [!div class="checklist"]
> - 创建项目
> - 配置窗口并添加文本
> - 添加按钮和代码
> - 调试并测试应用程序
> - 使用断点进行调试
> - 生成发布版本

## <a name="prerequisites"></a>必备条件

::: moniker range="vs-2017"
需要Visual Studio完成本教程。
请访问[Visual Studio下载页](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)，查看免费版本。
::: moniker-end
::: moniker range="vs-2019"
需要Visual Studio完成本教程。
请访问[Visual Studio下载页](https://visualstudio.microsoft.com/vs/)，查看免费版本。
::: moniker-end
::: moniker range=">=vs-2022"
需要Visual Studio完成本教程。
请访问[Visual Studio下载页](https://visualstudio.microsoft.com/downloads)，查看免费版本。
::: moniker-end

## <a name="create-the-project"></a>创建项目

在应用程序中创建Visual Studio，首先创建一个项目。
在本教程中，创建一Windows Presentation Foundation项目。

::: moniker range="vs-2017"
1. 打开 Visual Studio。

1. 在菜单栏上，选择"**文件** > **""新建** > **Project"。**

   ![屏幕截图显示Visual Studio文件"，然后选择"新建Project菜单中选择"新建"。](media/tutorial-wpf/visual-studio-create-project.png)

1. 在"**新建Project"** 对话框中，选择"已安装  >    >  **Visual Basic Windows桌面**"，然后选择 **"WPF 应用** (.NET Framework) 模板。 将项目命名为“HelloWPFApp”并选择“确定”。

   ![屏幕截图显示了"新建Project"对话框，该对话框选择了"W P F"应用模板。](media/tutorial-wpf/create-desktop-project.png)

   Visual Studio创建 HelloWPFApp 项目和解决方案。
   **解决方案资源管理器** 显示各种文件。

   ![屏幕截图解决方案资源管理器加载了 Hello W P F 应用文件。](media/tutorial-wpf/solution-explorer.png)

“WPF 设计器”在拆分视图中显示 MainWindow.xaml 的设计视图和 XAML 视图。
::: moniker-end
::: moniker range="vs-2019"
1. 打开 Visual Studio。

1. 在"**创建新项目"屏幕上**，搜索"WPF"，然后选择 **"WPF 应用** (.NET Framework) "。 选择“**下一页**”。

   !["创建新项目"对话框的屏幕截图，其中在搜索框中输入了 W P F，并且选择了"W P F 应用 (.NET Framework) 模板。](media/tutorial-wpf/visual-studio-create-wpf-project.png)

1. 为项目命名 *HelloWPFApp，* 然后选择"创建 **"。**

   Visual Studio创建 HelloWPFApp 项目和解决方案。
   **解决方案资源管理器** 显示各种文件。

   ![屏幕截图显示解决方案资源管理器 Hello W P F 应用文件。](media/tutorial-wpf/solution-explorer.png)

“WPF 设计器”在拆分视图中显示 MainWindow.xaml 的设计视图和 XAML 视图。
::: moniker-end

::: moniker range=">=vs-2022"
1. 打开 Visual Studio。
 
1. 在“开始”窗口上，选择“创建新项目”  。

   :::image type="content" source="media/vs-2022/start-window-create-new-project.png" alt-text="Visual Studio 2022 中的“开始”窗口的屏幕截图，其中突出显示了“创建新项目”选项。":::

1. 在"**创建新项目"窗口中**，搜索"WPF"，Visual Basic"所有语言 **"下拉列表中选择**"WPF"。
   选择“WPF 应用(.NET Framework)”，然后选择“下一步” 。

   :::image type="content" source="media/tutorial-wpf/visual-studio-create-wpf-project.png" alt-text="“创建新项目”对话框的屏幕截图，其中在搜索框中输入了 WPF，在语言列表中选择了 Visual Basic，并且突出显示了“WPF 应用(.NET Framework)”项目模板。":::

1. 为项目命名 **HelloWPFApp，** 然后选择"创建 **"。**

   Visual Studio创建 HelloWPFApp 项目和解决方案。
   **解决方案资源管理器** 显示各种文件。

   :::image type="content" source="media/vs-2022/explore-ide-hello-wpf-app-files.png" alt-text="显示解决方案资源管理器中的 HelloWPFApp 项目和解决方案中的文件的屏幕截图。":::

“WPF 设计器”在拆分视图中显示 MainWindow.xaml 的设计视图和 XAML 视图。
::: moniker-end

> [!NOTE]
> 有关 XAML (的可扩展应用程序标记语言) ，请参阅 WPF 的 [XAML 概述](/dotnet/framework/wpf/advanced/xaml-overview-wpf)。

## <a name="configure-window-and-add-text"></a>配置窗口并添加文本

使用 **"属性** "窗口，可以显示和更改项目项、控件和其他项的选项。

1. 在 **解决方案资源管理器** 中，打开 *MainWindow.xaml*。

1. 在 XAML 视图中，将 **Window.Title** 属性的值从 *Title="MainWindow"* 更改为 *Title="Greetings"。*

1. 在 IDE 的左侧Visual Studio"工具箱 **"** 选项卡。如果看不到它，请从菜单栏中选择"**查看** 工具箱 > "，或 **按 Ctrl** + **Alt** + **X**。

1. 展开" **常见 WPF 控件"，** 或在搜索 *栏中输入"* 文本"以 **查找 TextBlock**。

   :::image type="content" source="media/tutorial-wpf/toolbox-tab-text-block.png" alt-text="显示“工具箱”窗口的屏幕截图，其中突出显示了常用 WPF 控件列表中的 TextBlock 控件。":::

1. 选择 **TextBlock** 项，并将其拖动到设计图面上的窗口。
   可以通过拖动 TextBlock 控件来移动它。
   使用指南放置控件。

   :::image type="content" source="media/tutorial-wpf/form-with-text-block.png" alt-text="显示位于 Greetings 窗体上的 TextBlock 控件和参考线的屏幕截图。":::

   XAML 标记应如以下示例所示：

   ```xaml
   <TextBlock HorizontalAlignment="Left" Margin="381,100,0,0" TextWrapping="Wrap" Text="TextBlock" VerticalAlignment="Top"/>
   ```

1. 在 XAML 视图中，找到 TextBlock 的标记并更改 **Text** 属性：

   ```xaml
   Text="Select a message option and then choose the Display button."
   ```

   如有必要，再次将 TextBlock 居中

1. 通过选择"全部保存" **工具栏按钮保存** 应用。
   或者，若要保存应用，**请从菜单** 栏中选择"文件  >  **全部** 保存"，或按 **Ctrl** + **Shift** + **S**。
   最佳做法是尽早且经常保存。

## <a name="add-buttons-and-code"></a>添加按钮和代码

应用程序使用两个单选按钮和一个按钮。
使用以下步骤添加它们。
你将向按钮Visual Basic代码。
该代码引用单选按钮选择。

1. 在" **工具箱"** 中，找到 **RadioButton**。

   :::image type="content" source="media/tutorial-wpf/toolbox-radio-button.png" alt-text="显示“工具箱”窗口的屏幕截图，其中选择了常用 WPF 控件列表中的 RadioButton 控件。":::

1. 通过选择 RadioButton 项并拖动到设计图面，将两个 **RadioButton** 控件添加到设计图面。
   选择按钮，然后使用箭头键移动按钮。
   将按钮并排放在 TextBlock 控件下。

   :::image type="content" source="media/tutorial-wpf/greetings-form-radio-buttons.png" alt-text="显示具有一个 TextBlock 控件和两个单选按钮的 Greetings 窗体的屏幕截图。":::

1. 在 **左侧** RadioButton 控件的"属性"窗口中，将"属性"窗口顶部的"名称 **"** 属性更改为 *"HelloButton"。*

   :::image type="content" source="media/tutorial-wpf/properties-radio-button-name.png" alt-text="显示“HelloButton”RadioButton 的解决方案资源管理器“属性”窗口的屏幕截图。":::

1. 在右侧 RadioButton 控件的"属性"窗口中，将 **"名称"** 属性更改为 *"GoodbyeButton"。*

1. 在 XAML 中将 和 的 **Content** 属性 `HelloButton` `GoodbyeButton` `"Hello"` `"Goodbye"` 更新为 和 。

   ```xaml
   <Grid>
        <TextBlock HorizontalAlignment="Left" Margin="252,47,0,0" TextWrapping="Wrap" Text="Select a message option and then choose the Display button." VerticalAlignment="Top"/>
        <RadioButton x:Name="HelloButton" Content="Hello" HorizontalAlignment="Left" Margin="297,161,0,0" VerticalAlignment="Top"/>
        <RadioButton x:Name="GoodbyeButton" Content="Goodbye" HorizontalAlignment="Left" Margin="488,161,0,0" VerticalAlignment="Top"/>
   </Grid>
   ```

1. 在 XAML 视图中，找到 HelloButton 的标记并添加“IsChecked”属性：

   ```xaml
   IsChecked="True"
   ```

   **值为 True 的 IsChecked** 属性表示默认情况下已选中 HelloButton。 
   此设置意味着即使程序启动，也始终选中单选按钮。

1. 在" **工具箱"** 中，找到 **"按钮** "控件，然后将按钮拖动到 RadioButton 控件下的设计图面。

1. 在 XAML 视图中，将"按钮"控件的 **"** 内容"值从 更改为 `Content="Button"` `Content="Display"` 。

   ```xaml
   <Button Content="Display" HorizontalAlignment="Left" VerticalAlignment="Top" Width="75" Margin="215,204,0,0"/>
   ```

   你的窗口应类似于下图。

   :::image type="content" source="media/tutorial-wpf/greetings-buttons.png" alt-text="显示具有 TextBlock、标记为“Hello”和“Goodbye”的 RadioButtons 以及标记为“Display”的按钮控件的 Greetings 窗体的屏幕截图。":::

1. 在设计图面上，双击 **“显示”** 按钮。

   此时，“Greetings.xaml.vb”打开，光标位于 `Button_Click` 事件上。

    ```vb
    Private Sub Button_Click(sender As Object, e As RoutedEventArgs)

    End Sub
    ```

1. 添加以下代码：

    ```vb
    If HelloButton.IsChecked = True Then
        MessageBox.Show("Hello.")
    ElseIf GoodbyeButton.IsChecked = True Then
        MessageBox.Show("Goodbye.")
    End If
    ```

## <a name="debug-and-test-the-application"></a>调试并测试应用程序

接下来将调试应用程序，查找错误并测试两个消息框是否正确显示。
为了了解此过程的工作原理，第一步特意将错误引入程序。

1. 在“解决方案资源管理器”中，右键单击“MainWindow.xaml”，然后选择“重命名”。 将该文件重命名为“Greetings.xaml”。

1. 通过按 F5或选择“调试”，然后选择“启动调试”，启动调试程序。

   " **中断模式** " 窗口随即出现，" **输出** " 窗口指示发生了异常。

   :::image type="content" source="media/tutorial-wpf/exception-unhandled.png" alt-text="显示“异常未处理”窗口的屏幕截图，其中包含一条 System.IO.Exception 消息，内容为“无法定位资源 mainwindow.xaml”。":::

1. 依次选择“调试” > “停止调试”，停止调试程序。

   你已在本节开头将 *mainwindow.xaml* 重命名为 " *问候语* "。
   此代码仍引用 *mainwindow.xaml* 作为应用程序的启动 URI，因此无法启动该项目。

1. 在“解决方案资源管理器”中，打开“Application.xaml”文件。

1. 将 `StartupUri="MainWindow.xaml"` 更改为 `StartupUri="Greetings.xaml"`

1. 再次启动调试程序 （按“F5”）。 你现在应该可以看到应用程序的 Greetings 窗口。

   ::: moniker range="vs-2017"

   ![带有 TextBlock、单选按钮和 Button 控件的问候窗口屏幕截图。 已选择 "Hello" 单选按钮。](media/exploreide-wpf-running-app.png)

   ::: moniker-end

   ::: moniker range="vs-2019"

   ![带有 TextBlock、单选按钮和 Button 控件的问候窗口屏幕截图。 已选择 "Hello" 单选按钮。](media/vs-2019/exploreide-wpf-running-app.png)

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   :::image type="content" source="media/vs-2022/explore-ide-wpf-running-app.png" alt-text="Greetings 窗口的屏幕截图，其中显示了 TextBlock、RadioButtons 和 Button 控件，并选择了“Hello”单选按钮。":::

   ::: moniker-end

1. 选择 " **Hello** " 和 " **显示** " 按钮 **，然后单击** " **显示** " 按钮。
   使用右上角的 "关闭" 图标来停止调试。

有关详细信息，请参阅 [生成 wpf 应用程序 (wpf) ](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf) 和 [调试 wpf](../../debugger/debugging-wpf.md)。

## <a name="debug-with-breakpoints"></a>使用断点进行调试

可通过添加一些断点，在调试期间测试代码。

1. 打开“Greetings.xaml.vb”，并选择以下行：`MessageBox.Show("Hello.")`

1. 按 **F9** 添加断点或选择 " **调试**"，然后选择 " **切换断点**"。

   编辑器窗口的左边距中的代码行的旁边会出现一个红色圆圈。

1. 选择以下行： `MessageBox.Show("Goodbye.")`。

1. 按“F9”键添加断点，然后按“F5”启动调试。

1. 在 **问候语** 窗口中，选择 " **Hello** " 按钮，然后选择 " **显示**"。

   行 `MessageBox.Show("Hello.")` 将用黄色突出显示。
   在 IDE 底部，"自动 **"、"****局部变量**" 和 "**监视**" 窗口将停靠在左侧。
   "**调用堆栈**"、"**断点**"、"**异常设置**"、"**命令**"、"**即时**" 和 "**输出**" 窗口一起停靠在右侧。

   :::image type="content" source="media/vs-2022/explore-ide-debug-breakpoint.png" alt-text="显示 Visual Studio 中具有“代码，诊断”的调试会话的屏幕截图。“自动变量”和“调用堆栈”窗口处于打开状态。执行在 Greetings.xaml.vb 中的断点处停止。":::

1. 在菜单栏上，选择“调试” > “跳出”。

   应用程序将重新启动。
   随即出现一个对话框，其中显示 "Hello" 一词。

1. 选择“确定”按钮关闭对话框。

1. 在 **“Greetings”** 窗口中，选择 **“Goodbye”** 单选按钮，然后选择 **“显示”** 按钮。

   行 `MessageBox.Show("Goodbye.")` 将用黄色突出显示。

1. 按“F5”键继续调试。
   当对话框出现时，请选择 **"确定"** 以关闭对话框。

1. 关闭应用程序窗口，停止调试。

1. 在菜单栏上，选择“调试” > “禁用所有断点”。

## <a name="build-a-release-version"></a>生成发布版本

现在，你已验证一切正常，可以准备好应用程序的发布版本。

1. 选择 "**生成**  >  **干净解决方案**" 以删除在以前的生成过程中创建的中间文件和输出文件。

1. 使用工具栏上的下拉控件，将 HelloWPFApp 的生成配置从 " **调试** " 更改为 " **发布** "。

1. 选择“生成” > “生成解决方案”。

恭喜你完成本教程！
可在解决方案和项目目录 (...\HelloWPFApp\HelloWPFApp\bin\Release) 下找到生成的 .exe 文件。

## <a name="next-steps"></a>后续步骤

转到下一篇文章，了解如何使用 Visual Basic 在 Visual Studio 中创建 Windows 窗体应用。
> [!div class="nextstepaction"]
> [创建 Windows 窗体应用程序](../../ide/create-a-visual-basic-winform-in-visual-studio.md)

## <a name="see-also"></a>另请参阅

有关 Visual Studio 的详细信息，请参阅以下资源：

::: moniker range="vs-2017"
- [Visual Studio 2017 中的新增功能](../../ide/whats-new-visual-studio-2017.md)
- [工作效率提示](../../ide/productivity-features.md)
::: moniker-end
::: moniker range="vs-2019"
- [Visual Studio 2019 中的新增功能](../../ide/whats-new-visual-studio-2019.md)
- [工作效率提示](../../ide/productivity-features.md)
::: moniker-end
::: moniker range="vs-2022"
- [Visual Studio 2022 中的新增功能](../../ide/whats-new-visual-studio-2022.md)
- [工作效率提示](../../ide/productivity-features.md)
::: moniker-end
