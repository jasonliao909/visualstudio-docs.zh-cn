---
title: 使用 Visual Basic 和 WPF 生成 Hello World 应用
description: 使用 Visual Basic 在 Visual Studio 中通过 Windows Presentation Foundation (WPF) UI 框架创建简单的 Windows Desktop .NET 应用。
ms.custom: vs-acquisition, get-started
ms.date: 09/14/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
dev_langs:
- VB
ms.assetid: f84339c7-d617-4f56-bfcd-af2215c347ba
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: e96d0b52af0931c8d239d77381682d08c1b95462
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129972877"
---
# <a name="tutorial-create-a-simple-application-with-visual-basic"></a>教程：使用 Visual Basic 创建简单应用

通过完成本教程，你将熟悉在使用 Visual Studio 开发应用程序时可使用的许多工具、对话框和设计器。 你将创建“Hello, World”应用程序、设计 UI、添加代码并调试错误。在此期间，你将了解如何使用集成开发环境 ([IDE](visual-studio-ide.md))。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range=">=vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

## <a name="configure-the-ide"></a>配置 IDE

::: moniker range="vs-2017"

首次打开 Visual Studio 时，系统会提示你登录。 在本教程中，此步骤为可选步骤。 接下来可能会显示一个对话框，让你选择开发设置和颜色主题。 保留默认值，然后选择“启动 Visual Studio”。

![选择设置对话框](../media/exploreide-settings.png)

启动 Visual Studio 后，将看到工具窗口、菜单和工具栏，以及主窗口空间。 工具窗口停靠在应用程序窗口的左侧和右侧，其顶部有 **“快速启动”** 、菜单栏和标准工具栏。 应用程序窗口的中心是 **“起始页”** 。 当您加载解决方案或项目时，编辑器和设计器将显示在 **起始页** 的空间中。 开发应用程序时，大部分时间都将用在此中心区域。

![应用了常规设置的 Visual Studio 2017 IDE](../media/exploreide-idewithgeneralsettings.png)

::: moniker-end

::: moniker range=">=vs-2019"

启动 Visual Studio 时，“启动”窗口首先打开。 选择“继续但无需代码”打开开发环境。 将看到工具窗口、菜单和工具栏，以及主窗口空间。 工具窗口位于应用程序窗口的左右两侧。 搜索框、菜单栏和标准工具栏位于顶部。 加载解决方案或项目时，编辑器和设计器显示在应用程序窗口中间。 开发应用程序时，大部分时间都将用在此中心区域。

::: moniker-end

## <a name="create-the-project"></a>创建项目

在 Visual Studio 中创建应用程序时，应首先创建项目和解决方案。 此示例将创建一个 Windows Presentation Foundation (WPF) 项目。

::: moniker range="vs-2017"

1. 创建新项目。 在菜单栏中，选择“文件” > “新建” > “项目”  。

     ![在菜单栏上，依次选择“文件”、“新建”和“项目”](../media/exploreide-filenewproject.png)

1. 在“新项目”对话框中，依次选择“已安装” > “Visual Basic” > “Windows 桌面”类别和“WPF 应用(.NET Framework)”模板。 将项目命名为“HelloWPFApp”并选择“确定”。

     ![Visual Studio“新建项目”对话框中的 WPF 应用模板](media/exploreide-newproject-vb.png)

Visual Studio 将创建 HelloWPFApp 项目和解决方案，“解决方案资源管理器”将显示各种文件。 “WPF 设计器”在拆分视图中显示 MainWindow.xaml 的设计视图和 XAML 视图。 您可以滑动拆分器，以显示任一视图的更多或更少部分。 您可以选择只查看可视化视图或 XAML 视图。 **“解决方案资源管理器”** 中显示以下项：

![已加载 HelloWPFApp 文件的解决方案资源管理器](../media/exploreide-hellowpfappfiles.png)

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio。

1. 在“创建新项目”屏幕上，搜索“WPF”，选择“WPF App (.NET Framework)”，然后选择“下一步”。

   ![“创建新项目”对话框的屏幕截图，其中在搜索框中输入了 WPF，并选择了“WPF 应用(.NET Framework)”项目模板。](media/vs-2019/exploreide-newprojectvb-vs2019.png)

1. 在下一个屏幕中，为项目指定名称“HelloWPFApp”，然后选择“创建”。

Visual Studio 将创建 HelloWPFApp 项目和解决方案，“解决方案资源管理器”将显示各种文件。 “WPF 设计器”在拆分视图中显示 MainWindow.xaml 的设计视图和 XAML 视图。 您可以滑动拆分器，以显示任一视图的更多或更少部分。 您可以选择只查看可视化视图或 XAML 视图。 **“解决方案资源管理器”** 中显示以下项：

![显示解决方案资源管理器中的 HelloWPFApp 项目和解决方案中的文件的屏幕截图。](../media/vs-2019/exploreide-hellowpfappfiles.png)

::: moniker-end

::: moniker range=">=vs-2022"

1. 打开 Visual Studio。
 
1. 在“开始”窗口上，选择“创建新项目”  。

   :::image type="content" source="media/vs-2022/start-window-create-new-project.png" alt-text="Visual Studio 2022 中的“开始”窗口的屏幕截图，其中突出显示了“创建新项目”选项。":::

1. 在“创建新项目”屏幕上，搜索 WPF，并在“所有语言”下拉列表中选择 Visual Basic  。 选择“WPF 应用(.NET Framework)”，然后选择“下一步” 。

   :::image type="content" source="media/vs-2022/explore-ide-new-wpf-app-project-vb.png" alt-text="“创建新项目”对话框的屏幕截图，其中在搜索框中输入了 WPF，在语言列表中选择了 Visual Basic，并且突出显示了“WPF 应用(.NET Framework)”项目模板。":::

1. 在下一个屏幕中，为项目指定名称“HelloWPFApp”，然后选择“创建”。

Visual Studio 将创建 HelloWPFApp 项目和解决方案，“解决方案资源管理器”将显示各种文件。 “WPF 设计器”在拆分视图中显示 MainWindow.xaml 的设计视图和 XAML 视图。 您可以滑动拆分器，以显示任一视图的更多或更少部分。 您可以选择只查看可视化视图或 XAML 视图。 **“解决方案资源管理器”** 中显示以下项：

:::image type="content" source="media/vs-2022/explore-ide-hello-wpf-app-files.png" alt-text="显示解决方案资源管理器中的 HelloWPFApp 项目和解决方案中的文件的屏幕截图。":::

::: moniker-end

> [!NOTE]
> 若要详细了解 XAML (eXtensible Application Markup Language)，请参阅 [WPF 的 XAML 概述](/dotnet/framework/wpf/advanced/xaml-overview-wpf)页。

你可以在创建项目后进行自定义。 通过使用 **属性** 窗口（ **视图** 菜单上），您可以显示和更改应用程序中的项目项、控件和其他项的选项。

### <a name="change-the-name-of-mainwindowxaml"></a>更改 MainWindow.xaml 的名称

为 MainWindow 指定更具体的名称。 在“解决方案资源管理器”中，右键单击“MainWindow.xaml”，然后选择“重命名”。 将该文件重命名为“Greetings.xaml”。

你可以执行以下可选步骤来避免混淆：将应用程序窗口的标题更改为与此新名称一致。

1. 在“解决方案资源管理器”中，打开你刚才重命名的 Greetings.xaml 文件。

1. 在 XAML 视图中，将 Window.Title 属性的值从 `Title="MainWindow"` 更改为 `Title="Greetings"`，并保存更改。

## <a name="design-the-user-interface-ui"></a>设计用户界面 (UI)

如果设计器未打开，请在“解决方案资源管理器”中选择“Greetings.xaml”，然后按“Shift+F7”打开设计器。

我们会将三种类型的控件添加到此应用程序：一个 <xref:System.Windows.Controls.TextBlock> 控件、两个 <xref:System.Windows.Controls.RadioButton> 控件和一个 <xref:System.Windows.Controls.Button> 控件。

### <a name="add-a-textblock-control"></a>添加 TextBlock 控件

::: moniker range="vs-2019"

1. 按“Ctrl+Q”激活搜索框，然后键入“工具箱”  。 从结果列表中选择“查看”>“工具箱”。

1. 在“工具箱”中，展开“公共 WPF 控件”节点以查看 TextBlock 控件。

   ![显示“工具箱”窗口的屏幕截图，其中突出显示了常用 WPF 控件列表中的 TextBlock 控件。](../media/exploreide-textblocktoolbox.png)

1. 通过选择“TextBlock”项并将其拖到设计图面的窗口中，将 TextBlock 控件添加到设计图面中。 把控件居中到窗口的顶部附近。 在 Visual Studio 2019 和更高版本中，可以使用红色参考线来使控件居中。

你的窗口应与下图类似：

![显示位于 Greetings 窗体上的 TextBlock 控件的屏幕截图。](../media/exploreide-greetingswithtextblockonly.png)

XAML 标记应如下面的示例所示：

```xaml
<TextBlock HorizontalAlignment="Left" Margin="381,100,0,0" TextWrapping="Wrap" Text="TextBlock" VerticalAlignment="Top"/>
```

::: moniker-end

::: moniker range=">=vs-2022"

1. 按“Ctrl+Q”激活搜索框，然后键入“工具箱”  。 从结果列表中选择“查看”>“工具箱”。

1. 在“工具箱”中，展开“公共 WPF 控件”节点以查看 TextBlock 控件。

   :::image type="content" source="media/vs-2022/explore-ide-textblock-toolbox.png" alt-text="显示“工具箱”窗口的屏幕截图，其中突出显示了常用 WPF 控件列表中的 TextBlock 控件。":::

1. 通过选择“TextBlock”项并将其拖到设计图面的窗口中，将 TextBlock 控件添加到设计图面中。 把控件居中到窗口的顶部附近。 可以使用参考线将控件居中。

你的窗口应类似于下图：

:::image type="content" source="media/vs-2022/explore-ide-greetings-with-textblock-only.png" alt-text="显示位于 Greetings 窗体上的 TextBlock 控件和参考线的屏幕截图。":::

XAML 标记应如下面的示例所示：

```xaml
<TextBlock HorizontalAlignment="Left" Margin="381,100,0,0" TextWrapping="Wrap" Text="TextBlock" VerticalAlignment="Top"/>
```

::: moniker-end

### <a name="customize-the-text-in-the-text-block"></a>自定义文本块中的文本

1. 在 XAML 视图中，找到 TextBlock 的标记并更改 Text 属性：

   ```xaml
   Text="Select a message option and then choose the Display button."
   ```

1. 视需要再次使 TextBlock 居中，并通过按 Ctrl+S 或使用“文件”菜单项保存更改。

接下来，向窗体添加两个 [RadioButton](/dotnet/framework/wpf/controls/radiobutton) 控件。

### <a name="add-radio-buttons"></a>添加单选按钮

::: moniker range="vs-2019"

1. 在“工具箱”中，查找“RadioButton”控件。

     ![显示“工具箱”窗口的屏幕截图，其中选择了常用 WPF 控件列表中的 RadioButton 控件。](../media/exploreide-radiobuttontoolbox.png)

1. 通过选择“RadioButton”项并将其拖到设计图面的窗口中，将两个 RadioButton 控件添加到设计图面中。 移动按钮（通过选择它们并使用箭头键），以便按钮并排显示在 TextBlock 控件下。 使用红色参考线来对齐控件。

     你的窗口应如下所示：

     ![显示具有一个 TextBlock 控件和两个单选按钮的 Greetings 窗体的屏幕截图。](../media/exploreide-greetingswithradiobuttons.png)

1. 在左侧 RadioButton 控件的 **“属性”** 窗口中，将 **“名称”** 属性（位于 **“属性”** 窗口顶部）更改为 `HelloButton`。

     ![显示“HelloButton”RadioButton 的解决方案资源管理器“属性”窗口的屏幕截图。](../media/exploreide-buttonproperties.png)

1. 在右侧 RadioButton 控件的“属性”窗口中，将“名称”属性更改为 `GoodbyeButton`，然后保存更改。

你现在可以为每个 RadioButton 控件添加显示文本。 以下程序将更新 RadioButton 控件的 **“内容”** 属性。

::: moniker-end

::: moniker range=">=vs-2022"

1. 在“工具箱”中，查找“RadioButton”控件。

     :::image type="content" source="media/vs-2022/explore-ide-radiobutton-toolbox.png" alt-text="显示“工具箱”窗口的屏幕截图，其中选择了常用 WPF 控件列表中的 RadioButton 控件。":::

1. 通过选择“RadioButton”项并将其拖到设计图面的窗口中，将两个 RadioButton 控件添加到设计图面中。 移动按钮（通过选择它们并使用箭头键），以便按钮并排显示在 TextBlock 控件下。 可使用参考线来对齐控件。

     你的窗口应如下所示：

     :::image type="content" source="media/vs-2022/explore-ide-greetings-with-radiobuttons.png" alt-text="显示具有一个 TextBlock 控件和两个单选按钮的 Greetings 窗体的屏幕截图。":::

1. 在左侧 RadioButton 控件的 **“属性”** 窗口中，将 **“名称”** 属性（位于 **“属性”** 窗口顶部）更改为 `HelloButton`。

     :::image type="content" source="media/vs-2022/explore-ide-button-properties.png" alt-text="显示“HelloButton”RadioButton 的解决方案资源管理器“属性”窗口的屏幕截图。":::

1. 在右侧 RadioButton 控件的“属性”窗口中，将“名称”属性更改为 `GoodbyeButton`，然后保存更改。

你现在可以为每个 RadioButton 控件添加显示文本。 以下程序将更新 RadioButton 控件的 **“内容”** 属性。

::: moniker-end
### <a name="add-display-text-for-each-radio-button"></a>添加每个单选按钮的显示文本

在 XAML 中将`HelloButton` 和 `GoodbyeButton` 的“内容”属性更新为 `"Hello"` 和 `"Goodbye"`。 XAML 标记现在应类似于以下示例：

   ```xaml
   <Grid>
        <TextBlock HorizontalAlignment="Left" Margin="252,47,0,0" TextWrapping="Wrap" Text="Select a message option and then choose the Display button." VerticalAlignment="Top"/>
        <RadioButton x:Name="HelloButton" Content="Hello" HorizontalAlignment="Left" Margin="297,161,0,0" VerticalAlignment="Top"/>
        <RadioButton x:Name="GoodbyeButton" Content="Goodbye" HorizontalAlignment="Left" Margin="488,161,0,0" VerticalAlignment="Top"/>
   </Grid>
   ```

### <a name="set-a-radio-button-to-be-checked-by-default"></a>设置要默认选中的单选按钮

这一步将设置要默认选中的 HelloButton，这样两个单选按钮中始终有一个处于选中状态。

在 XAML 视图中，找到 HelloButton 的标记并添加“IsChecked”属性：

```xaml
IsChecked="True"
```

最后添加的 UI 元素是 [Button](/dotnet/framework/wpf/controls/button) 控件。

### <a name="add-the-button-control"></a>添加按钮控件

::: moniker range="vs-2019"

1. 在“工具箱”中，找到“按钮”控件，然后通过将控件拖到设计视图的窗体中，将其添加到 RadioButton 控件下方的设计界面中。 这些参考线可以帮助你将控件居中。

1. 在 XAML 视图中，将 Button 控件的“内容”值从 `Content="Button"` 更改为 `Content="Display"`，然后保存更改。

   标记应与以下示例类似：`<Button Content="Display" HorizontalAlignment="Left" VerticalAlignment="Top" Width="75" Margin="215,204,0,0"/>`

   你的窗口应与下图类似。

   ![显示具有 TextBlock、标记为“Hello”和“Goodbye”的 RadioButtons 以及标记为“Display”的按钮控件的 Greetings 窗体的屏幕截图。](../media/exploreide-greetingswithcontrollabels.png)

::: moniker-end

::: moniker range=">=vs-2022"

1. 在“工具箱”中，找到“按钮”控件，然后通过将控件拖到设计视图的窗体中，将其添加到 RadioButton 控件下方的设计界面中。 这些参考线可以帮助你将控件居中。

1. 在 XAML 视图中，将 Button 控件的“内容”值从 `Content="Button"` 更改为 `Content="Display"`，然后保存更改。

   标记应与以下示例类似：

   ```xaml
   <Button Content="Display" HorizontalAlignment="Left" VerticalAlignment="Top" Width="75" Margin="215,204,0,0"/>
   ```

   你的窗口应类似于下图。

   :::image type="content" source="media/vs-2022/explore-ide-greetings-with-control-labels.png" alt-text="显示具有 TextBlock、标记为“Hello”和“Goodbye”的 RadioButtons 以及标记为“Display”的按钮控件的 Greetings 窗体的屏幕截图。":::

::: moniker-end
### <a name="add-code-to-the-display-button"></a>向显示按钮添加代码

此应用程序运行时，用户选择单选按钮，再选择“显示” 按钮之后，会显示一个消息框。 选择 Hello 将显示一个消息框，选择 Goodbye 将显示另一个。 要创建此行为，需将代码添加到 Greetings.xaml.vb 或 Greetings.xaml.cs 中的 `Button_Click` 事件。

1. 在设计图面上，双击 **“显示”** 按钮。

     此时，“Greetings.xaml.vb”打开，光标位于 `Button_Click` 事件上。

    ```vb
    Private Sub Button_Click(sender As Object, e As RoutedEventArgs)

    End Sub
    ```

1. 输入以下代码：

    ```vb
    If HelloButton.IsChecked = True Then
        MessageBox.Show("Hello.")
    ElseIf GoodbyeButton.IsChecked = True Then
        MessageBox.Show("Goodbye.")
    End If
    ```

1. 保存应用程序。

## <a name="debug-and-test-the-application"></a>调试并测试应用程序

接下来将调试应用程序，查找错误并测试两个消息框是否正确显示。 下面的说明介绍如何生成和启动调试器，但以后可以阅读[生成 WPF 应用程序 (WPF)](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf) 和[调试 WPF](../../debugger/debugging-wpf.md) 获取有关详细信息。

### <a name="find-and-fix-errors"></a>查找并修复错误

在此步骤中，将遇到之前因更改 MainWindow.xaml 文件的名称而引起的错误。

#### <a name="start-debugging-and-find-the-error"></a>开始调试和查找错误

::: moniker range="vs-2019"

1. 通过按 F5或选择“调试”，然后选择“启动调试”，启动调试程序。

   将出现“中断模式”窗口，“输出”窗口指示发生 IOException :“找不到资源 'mainwindow.xaml'”。

   ![显示“异常未处理”窗口的屏幕截图，其中包含一条 System.IO.Exception 消息，内容为“无法定位资源 mainwindow.xaml”。](../media/exploreide-ioexception.png)

1. 依次选择“调试”>“停止调试”，停止调试器 。

开始学习本教程时，我们将 MainWindow.xaml 重命名为 Greetings.xaml，但是该代码仍然引用 MainWindow.xaml 作为应用程序的启动 URI，因此该项目无法启动。

::: moniker-end

::: moniker range=">=vs-2022"

1. 通过按 F5或选择“调试”，然后选择“启动调试”，启动调试程序。

   将出现“中断模式”窗口，“输出”窗口指示发生 IOException :“找不到资源 'mainwindow.xaml'”。

   :::image type="content" source="media/vs-2022/explore-ide-ioexception.png" alt-text="显示“异常未处理”窗口的屏幕截图，其中包含一条 System.IO.Exception 消息，内容为“无法定位资源 mainwindow.xaml”。":::

1. 依次选择“调试”>“停止调试”，停止调试器 。

开始学习本教程时，我们将 MainWindow.xaml 重命名为 Greetings.xaml，但是该代码仍然引用 MainWindow.xaml 作为应用程序的启动 URI，因此该项目无法启动。

::: moniker-end

#### <a name="specify-greetingsxaml-as-the-startup-uri"></a>将 Greetings.xaml 指定为启动 URI

1. 在“解决方案资源管理器”中，打开“Application.xaml”文件。

1. 将 `StartupUri="MainWindow.xaml"` 更改为 `StartupUri="Greetings.xaml"`，然后保存更改。

再次启动调试程序 （按“F5”）。 你现在应该可以看到应用程序的 Greetings 窗口。

::: moniker range="vs-2017"

![正在运行的应用的屏幕截图](media/exploreide-wpf-running-app.png "Greetings 窗口的屏幕截图，其中显示了 TextBlock、RadioButtons 和按钮控件，并选择了“Hello”单选按钮。")

::: moniker-end

::: moniker range="vs-2019"

![正在运行的应用的屏幕截图](media/vs-2019/exploreide-wpf-running-app.png "Greetings 窗口的屏幕截图，其中显示了 TextBlock、RadioButtons 和按钮控件，并选择了“Hello”单选按钮。")

::: moniker-end

::: moniker range=">=vs-2022"

:::image type="content" source="media/vs-2022/explore-ide-wpf-running-app.png" alt-text="Greetings 窗口的屏幕截图，其中显示了 TextBlock、RadioButtons 和 Button 控件，并选择了“Hello”单选按钮。":::

::: moniker-end

现在关闭应用程序窗口，停止调试。

### <a name="debug-with-breakpoints"></a>使用断点进行调试

可通过添加一些断点，在调试期间测试代码。 可以通过选择“调试” > “切换断点”、通过在编辑器中想要添加断点的代码行旁边的左边距中单击或按 F9 来添加断点。

#### <a name="add-breakpoints"></a>添加断点

::: moniker range="vs-2019"

1. 打开“Greetings.xaml.vb”，并选择以下行：`MessageBox.Show("Hello.")`

1. 通过按 F9 或从菜单选择“调试”，然后选择“切换断点”添加断点。

   编辑器窗口最左侧边距中该代码行附近将显示一个红圈。

1. 选择以下行： `MessageBox.Show("Goodbye.")`。

1. 按“F9”键添加断点，然后按“F5”启动调试。

1. 在 **“Greetings”** 窗口中，选择 **“Hello”** 单选按钮，然后选择 **“显示”** 按钮。

   行 `MessageBox.Show("Hello.")` 将用黄色突出显示。 在 IDE 底部，“自动”、“本地”和“监视”窗口一起停靠在左侧，而“调用堆栈”、“断点”、“异常设置”、“命令”、“即时”和“输出”窗口一起停靠在右侧。

   ![显示 Visual Studio 中具有“代码，诊断”的调试会话的屏幕截图。 “自动变量”和“调用堆栈”窗口处于打开状态。 执行在 Greetings.xaml.vb 中的断点处停止。](media/exploreide-debugbreakpoint.png)

1. 在菜单栏上，选择“调试”>“跳出” 。

     应用程序继续执行，并将显示出带有“Hello”的消息框。

1. 选择消息框上的 **“确定”** 按钮将其关闭。

1. 在 **“Greetings”** 窗口中，选择 **“Goodbye”** 单选按钮，然后选择 **“显示”** 按钮。

     行 `MessageBox.Show("Goodbye.")` 将用黄色突出显示。

1. 按“F5”键继续调试。 当消息框出现时，选择消息框上的 **“确定”** 按钮将其关闭。

1. 关闭应用程序窗口，停止调试。

1. 在菜单栏上，选择“调试”>“禁用所有断点” 。

::: moniker-end

::: moniker range=">=vs-2022"

1. 打开“Greetings.xaml.vb”，并选择以下行：`MessageBox.Show("Hello.")`

1. 通过按 F9 或从菜单选择“调试”，然后选择“切换断点”添加断点。

   编辑器窗口最左侧边距或装订线中的代码行附近将显示一个红圈。

1. 选择以下行： `MessageBox.Show("Goodbye.")`。

1. 按“F9”键添加断点，然后按“F5”启动调试。

1. 在 **“Greetings”** 窗口中，选择 **“Hello”** 单选按钮，然后选择 **“显示”** 按钮。

   行 `MessageBox.Show("Hello.")` 将用黄色突出显示。 在 IDE 底部，“自动”、“本地”和“监视”窗口一起停靠在左侧，而“调用堆栈”、“断点”、“异常设置”、“命令”、“即时”和“输出”窗口一起停靠在右侧。

   :::image type="content" source="media/vs-2022/explore-ide-debug-breakpoint.png" alt-text="显示 Visual Studio 中具有“代码，诊断”的调试会话的屏幕截图。“自动变量”和“调用堆栈”窗口处于打开状态。执行在 Greetings.xaml.vb 中的断点处停止。":::

1. 在菜单栏上，选择“调试”>“跳出” 。

     应用程序继续执行，并将显示出带有“Hello”的消息框。

1. 选择消息框上的 **“确定”** 按钮将其关闭。

1. 在 **“Greetings”** 窗口中，选择 **“Goodbye”** 单选按钮，然后选择 **“显示”** 按钮。

     行 `MessageBox.Show("Goodbye.")` 将用黄色突出显示。

1. 按“F5”键继续调试。 当消息框出现时，选择消息框上的 **“确定”** 按钮将其关闭。

1. 关闭应用程序窗口，停止调试。

1. 在菜单栏上，选择“调试”>“禁用所有断点” 。

::: moniker-end

### <a name="view-a-representation-of-the-ui-elements"></a>查看 UI 元素的表示形式

在正在运行的应用中，你会看到窗口顶部显示了一个小组件。 这是一个运行时帮助程序，通过它可以快速访问一些有用的调试功能。 单击第一个按钮“转到实时可视化树”。 随即会看到一个包含一个树的窗口，树中包含页面的所有可视元素。 展开节点，找到你添加的按钮。

::: moniker range="vs-2019"

![显示“实时视觉对象树”窗口的屏幕截图，其中显示了一个树，包含 HelloWPFApp.exe 的所有视觉对象元素。](media/vs-2019/exploreide-live-visual-tree.png)

::: moniker-end

::: moniker range=">=vs-2022"

:::image type="content" source="media/vs-2022/explore-ide-live-visual-tree.png" alt-text="显示“实时视觉对象树”窗口的屏幕截图，其中显示了一个树，包含 HelloWPFApp.exe 的所有视觉对象元素。":::

::: moniker-end
### <a name="build-a-release-version-of-the-application"></a>生成应用程序的发布版本

确认一切就绪后，可以准备该应用程序的发布版本。

1. 在主菜单中，依次选择“生成” > “清理解决方案”，删除上一生成过程中创建的中间文件和输出文件。 这不是必需的，但它会清理调试生成输出。

1. 使用工具栏（当前显示“调试”）上的下拉列表控件把 HelloWPFApp 的生成配置从“调试”更改为“发布” 。

1. 选择“生成” > “生成解决方案”来生成解决方案 。

恭喜你完成本教程！ 可在解决方案和项目目录 (...\HelloWPFApp\HelloWPFApp\bin\Release) 下找到生成的 .exe 文件。

## <a name="see-also"></a>另请参阅

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
