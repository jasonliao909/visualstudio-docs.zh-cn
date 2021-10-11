---
title: 使用 C# 和 WPF 生成 Hello World 应用
description: 使用 C# 在 Visual Studio 中通过 Windows Presentation Foundation (WPF) UI 框架创建简单的 Windows Desktop .NET 应用。
ms.custom: vs-acquisition, get-started
ms.date: 09/14/2021
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: tutorial
dev_langs:
- CSharp
ms.assetid: f84339c7-d617-4f56-bfcd-af2215c347ba
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 7627c96851133ba14f5fd3a2b59e3ca3f4e7e567
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128428483"
---
# <a name="tutorial-create-a-simple-application-with-c"></a>教程：使用 C\# 创建简单应用

通过完成本教程，你将熟悉在使用 Visual Studio 开发应用程序时可使用的许多工具、对话框和设计器。 你将创建“Hello, World”应用程序、设计 UI、添加代码并调试错误。在此期间，你将了解如何使用集成开发环境 ([IDE](visual-studio-ide.md))。

## <a name="prerequisites"></a>先决条件

::: moniker range="vs-2017"
如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?)页免费安装。
::: moniker-end
::: moniker range=">=vs-2019"

- 如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页免费安装。
- 在本教程中，可以使用 .NET Framework 或 .NET Core。 .NET Core 是较新的、更新式的框架。 .NET Core 需要 Visual Studio 2019 16.3 或更高版本。
::: moniker-end

## <a name="configure-the-ide"></a>配置 IDE

::: moniker range="vs-2017"

首次打开 Visual Studio 时，系统会提示你登录。 在本教程中，此步骤为可选步骤。 接下来可能会显示一个对话框，让你选择开发设置和颜色主题。 保留默认值，然后选择“启动 Visual Studio”。

![选择设置对话框](../media/exploreide-settings.png)

启动 Visual Studio 后，将看到工具窗口、菜单和工具栏，以及主窗口空间。 工具窗口停靠在应用程序窗口的左侧和右侧，其顶部有 **“快速启动”** 、菜单栏和标准工具栏。 应用程序窗口的中心是 **“起始页”** 。 当您加载解决方案或项目时，编辑器和设计器将显示在 **起始页** 的空间中。 开发应用程序时，大部分时间都将用在此中心区域。

![应用了常规设置的 Visual Studio 2017 IDE](../media/exploreide-idewithgeneralsettings.png "应用了常规设置的 Visual Studio 2017 IDE 的屏幕截图")

::: moniker-end

::: moniker range=">=vs-2019"

启动 Visual Studio 时，“启动”窗口首先打开。 选择“继续但无需代码”打开开发环境。 将看到工具窗口、菜单和工具栏，以及主窗口空间。 工具窗口位于应用程序窗口的左右两侧。 搜索框、菜单栏和标准工具栏位于顶部。 加载解决方案或项目时，编辑器和设计器显示在应用程序窗口中间。 开发应用程序时，大部分时间都将用在此中心区域。

::: moniker-end

## <a name="create-the-project"></a>创建项目

在 Visual Studio 中创建应用程序时，应首先创建项目和解决方案。 此示例将创建一个 Windows Presentation Foundation (WPF) 项目。

::: moniker range="vs-2017"

1. 创建新项目。 在菜单栏中，选择“文件” > “新建” > “项目”  。

     ![在菜单栏上，依次选择“文件”、“新建”、“项目”](../media/exploreide-filenewproject.png "显示可在其中选择“文件”、“新建”、“项目”的 Visual Studio 菜单栏的屏幕截图。")

1. 在“新建项目”对话框中，选择“已安装” > “Visual C#” > “Windows 桌面”类别，然后选择“WPF 应用(.NET Framework)”模板    。 将项目命名为“HelloWPFApp”并选择“确定”。

     ![Visual Studio“新建项目”对话框中的 WPF 应用模板](media/exploreide-newprojectcsharp.png "“新建项目”对话框中的 WPF 应用模板的屏幕截图。")

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio。

1. 在“开始”窗口上，选择“创建新项目”。

   ![查看“创建新项目”窗口](../../get-started/media/vs-2019/start-window-create-new-project.png "Visual Studio 2022 中的“开始”窗口的屏幕截图，其中突出显示了“创建新项目”选项。")

1. 在“创建新项目”屏幕上，搜索“WPF”，选择“WPF 应用程序”，然后选择“下一步”  。

   :::image type="content" source="media/vs-2019/explore-ide-new-project-csharp-vs-2019.png" alt-text="“创建新项目”对话框的屏幕截图，其中在搜索框中输入了“WPF”，并突出显示了“WPF 应用程序”项目模板。":::

1. 在下一个屏幕中，为项目指定名称“HelloWPFApp”，然后选择“下一步”。

   :::image type="content" source="./media/vs-2019/explore-ide-name-project.png" alt-text="“配置新项目”对话框的屏幕截图，其中在“项目名称”字段中输入了“HelloWPFApp”。":::

1. 在“附加信息”窗口中，应已为目标框架选择“.NET Core 3.1” 。 如果未选择，则请选择“.NET Core 3.1”。 然后，选择“创建”。

   :::image type="content" source="./media/vs-2019/wpf-target-framework.png" alt-text="在“附加信息”窗口中，确保已选择“.NET Core 3.1”":::

Visual Studio 将创建 HelloWPFApp 项目和解决方案，“解决方案资源管理器”将显示各种文件。 “WPF 设计器”在拆分视图中显示 MainWindow.xaml 的设计视图和 XAML 视图。 您可以滑动拆分器，以显示任一视图的更多或更少部分。 您可以选择只查看可视化视图或 XAML 视图。

![IDE 中的 WPF 项目和解决方案](media/exploreide-wpfproject-cs.png "Visual Studio IDE 中 HelloWPFApp 项目和解决方案的屏幕截图，其中打开了解决方案资源管理器，并且在 WPF 设计器中打开了“MainWindow.xaml”的 XAML 和设计器视图。")

> [!NOTE]
> 若要详细了解 XAML (eXtensible Application Markup Language)，请参阅 [WPF 的 XAML 概述](/dotnet/framework/wpf/advanced/xaml-overview-wpf)页。

你可以在创建项目后进行自定义。 若要执行此操作，请从“视图”菜单中选择“属性窗口”或按 F4  。 然后可显示和更改应用程序中的项目项、控件和其他项的选项。

![属性窗口](../media/exploreide-hellowpfappfiles.png "“解决方案资源管理器”窗口的屏幕截图，其中显示了 HelloWPF 应用中的属性、引用和文件。")

::: moniker-end

::: moniker range=">=vs-2022"

1. 打开 Visual Studio。

1. 在“开始”窗口上，选择“创建新项目”  。

   :::image type="content" source="media/vs-2022/start-window-create-new-project.png" alt-text="Visual Studio 2022 中的“开始”窗口的屏幕截图，其中突出显示了“创建新项目”选项。":::

1. 在“创建新项目”屏幕上，搜索“WPF”，选择“WPF 应用程序”，然后选择“下一步”  。

   :::image type="content" source="media/vs-2022/explore-ide-new-project-csharp-wpf-vs-2022.png" alt-text="“创建新项目”对话框的屏幕截图，其中在搜索框中输入了“WPF”，并突出显示了“WPF 应用程序”项目模板。":::

1. 在下一个屏幕中，为项目指定名称“HelloWPFApp”，然后选择“下一步”。

   :::image type="content" source="media/vs-2022/explore-ide-name-project.png" alt-text="“配置新项目”对话框的屏幕截图，其中在“项目名称”字段中输入了“HelloWPFApp”。":::

1. 在“其他信息”窗口中，应已选择“.NET 6.0”作为目标框架 。 如果未选择，请选择“.NET 6.0”。 然后，选择“创建”。

   :::image type="content" source="media/vs-2022/wpf-target-framework.png" alt-text="“其他信息”窗口的屏幕截图，其中在“框架”字段中选择了“.NET 6.0”。":::

Visual Studio 将创建 HelloWPFApp 项目和解决方案，“解决方案资源管理器”将显示各种文件。 “WPF 设计器”在拆分视图中显示 MainWindow.xaml 的设计视图和 XAML 视图。 您可以滑动拆分器，以显示任一视图的更多或更少部分。 您可以选择只查看可视化视图或 XAML 视图。

:::image type="content" source="media/vs-2022/explore-ide-wpf-project-cs.png" alt-text="Visual Studio IDE 中 HelloWPFApp 项目和解决方案的屏幕截图，其中打开了解决方案资源管理器，并在 WPF 设计器中打开了“MainWindow.xaml”的 XAML 和设计器视图。":::

> [!NOTE]
> 若要详细了解 XAML (eXtensible Application Markup Language)，请参阅 [WPF 的 XAML 概述](/dotnet/framework/wpf/advanced/xaml-overview-wpf)页。

你可以在创建项目后进行自定义。 若要执行此操作，请从“视图”菜单中选择“属性窗口”或按 F4  。 然后可显示和更改应用程序中的项目项、控件和其他项的选项。

:::image type="content" source="media/vs-2022/explore-ide-hello-wpf-properties.png" alt-text="“属性”窗口的屏幕截图，其中显示了 HelloWPFApp 项目的“解决方案属性”的“其他”部分。":::

::: moniker-end

### <a name="change-the-name-of-mainwindowxaml"></a>更改 MainWindow.xaml 的名称

为 MainWindow 指定更具体的名称。 在“解决方案资源管理器”中，右键单击“MainWindow.xaml”，然后选择“重命名”。 将该文件重命名为“Greetings.xaml”。

## <a name="design-the-user-interface-ui"></a>设计用户界面 (UI)

如果设计器未打开，请选择“Greetings.xaml”，然后按“Shift+F7”打开设计器 。

我们会将三种类型的控件添加到此应用程序：一个 <xref:System.Windows.Controls.TextBlock> 控件、两个 <xref:System.Windows.Controls.RadioButton> 控件和一个 <xref:System.Windows.Controls.Button> 控件。

### <a name="add-a-textblock-control"></a>添加 TextBlock 控件

::: moniker range="vs-2019"

1. 按“Ctrl+Q”激活搜索框，然后键入“工具箱”  。 从结果列表中选择“查看”>“工具箱”。

1. 在“工具箱”中，展开“公共 WPF 控件”节点以查看 TextBlock 控件。

     ![突出显示 TextBlock 控件的工具箱](../media/exploreide-textblocktoolbox.png "“工具箱”窗口的屏幕截图，其中在“常用 WPF 控件”列表中选择了 TextBlock 控件。")

1. 通过选择“TextBlock”项并将其拖到设计图面的窗口中，将 TextBlock 控件添加到设计图面中。 把控件居中到窗口的顶部附近。 在 Visual Studio 2019 和更高版本中，可以使用红色参考线来使控件居中。

    你的窗口应与下图类似：

    ![Greetings 窗体上的 TextBlock 控件](../media/exploreide-greetingswithtextblockonly.png "“Greetings”窗体设计图面上的 TextBlock 控件的屏幕截图。")

   XAML 标记应如下面的示例所示：

    ```xaml
    <Grid>
        <TextBlock HorizontalAlignment="Left" Margin="387,60,0,0" TextWrapping="Wrap" Text="TextBlock" VerticalAlignment="Top"/>
    </Grid>
    ```

::: moniker-end

::: moniker range=">=vs-2022"

1. 按“Ctrl+Q”激活搜索框，然后键入“工具箱”  。 从结果列表中选择“查看”>“工具箱”。

1. 在“工具箱”中，展开“公共 WPF 控件”节点以查看 TextBlock 控件。

    :::image type="content" source="media/vs-2022/explore-ide-textblock-toolbox.png" alt-text="“工具箱”窗口的屏幕截图，其中在“常用 WPF 控件”列表中选择了 TextBlock 控件。":::

1. 通过选择“TextBlock”项并将其拖到设计图面的窗口中，将 TextBlock 控件添加到设计图面中。 把控件居中到窗口的顶部附近。 可以使用参考线将控件居中。

    你的窗口应类似于下图：

    :::image type="content" source="media/vs-2022/explore-ide-greetings-with-textblock-only.png" alt-text="设计图面上的 TextBlock 控件的屏幕截图。显示了用于设定控件位置和调整控件大小的参考线。":::

   XAML 标记应如下面的示例所示：

    ```xaml
    <Grid>
        <TextBlock HorizontalAlignment="Left" Margin="387,60,0,0" TextWrapping="Wrap" Text="TextBlock" VerticalAlignment="Top"/>
    </Grid>
    ```

::: moniker-end

### <a name="customize-the-text-in-the-text-block"></a>自定义文本块中的文本

1. 在 XAML 视图中，找到 TextBlock 的标记并将 Text 属性从 `TextBox` 更改为 `Select a message option and then choose the Display button.` 

   XAML 标记应如下面的示例所示：

   ```xaml
   <Grid>
       <TextBlock HorizontalAlignment="Left" Margin="387,60,0,0" TextWrapping="Wrap" Text="Select a message option and then choose the Display button." VerticalAlignment="Top"/>
   </Grid>
   ```

1. 如果愿意，再次使 TextBlock 居中，然后通过按 Ctrl+S 或使用“文件” 菜单项保存更改。

接下来，向窗体添加两个 [RadioButton](/dotnet/framework/wpf/controls/radiobutton) 控件。

### <a name="add-radio-buttons"></a>添加单选按钮

::: moniker range="vs-2019"

1. 在“工具箱”中，查找“RadioButton”控件。

     ![选定 RadioButton 控件的“工具箱”窗口](../media/exploreide-radiobuttontoolbox.png "“工具箱”窗口的屏幕截图，其中在“常用 WPF 控件”列表中选择了 RadioButton 控件。")

1. 通过选择“RadioButton”项并将其拖到设计图面的窗口中，将两个 RadioButton 控件添加到设计图面中。 移动按钮（通过选择它们并使用箭头键），以便按钮并排显示在 TextBlock 控件下。 使用红色参考线来对齐控件。

   你的窗口应如下所示：

   ![包含 TextBlock 和两个单选按钮的“Greetings”窗体](../media/exploreide-greetingswithradiobuttons.png "Greetings.xaml 的“设计”窗口的屏幕截图，其中显示了位于设计图面上的一个 TextBlock 控件和两个 RadioButton 控件。")

1. 在左侧 RadioButton 控件的 **“属性”** 窗口中，将 **“名称”** 属性（位于 **“属性”** 窗口顶部）更改为 `HelloButton`。

    ![RadioButton 属性窗口](../media/exploreide-buttonproperties.png "RadioButton 控件的“属性”窗口的屏幕截图。Name 属性的值已更改为“HelloButton”。")

1. 在右侧 RadioButton 控件的“属性”窗口中，将“名称”属性更改为 `GoodbyeButton`，然后保存更改。

接下来，将为每个 RadioButton 控件添加显示文本。 以下程序将更新 RadioButton 控件的 **“内容”** 属性。

::: moniker-end

::: moniker range=">=vs-2022"

1. 在“工具箱”中，查找“RadioButton”控件。

   :::image type="content" source="media/vs-2022/explore-ide-radiobutton-toolbox.png" alt-text="“工具箱”窗口的屏幕截图，其中在“常用 WPF 控件”列表中选择了 RadioButton 控件。":::

1. 通过选择“RadioButton”项并将其拖到设计图面的窗口中，将两个 RadioButton 控件添加到设计图面中。 移动按钮（通过选择它们并使用箭头键），以便按钮并排显示在 TextBlock 控件下。 可以使用参考线来对齐控件。

   你的窗口应如下所示：

   :::image type="content" source="media/vs-2022/explore-ide-greetings-with-radiobuttons.png" alt-text="Greetings.xaml 的“设计”窗口的屏幕截图，其中显示了位于设计图面上的一个 TextBlock 控件和两个 RadioButton 控件。":::

1. 在左侧 RadioButton 控件的 **“属性”** 窗口中，将 **“名称”** 属性（位于 **“属性”** 窗口顶部）更改为 `HelloButton`。

   :::image type="content" source="media/vs-2022/explore-ide-button-properties.png" alt-text="RadioButton 控件的“属性”窗口的屏幕截图。Name 属性的值已更改为“HelloButton”。":::

1. 在右侧 RadioButton 控件的“属性”窗口中，将“名称”属性更改为 `GoodbyeButton`，然后保存更改。

接下来，将为每个 RadioButton 控件添加显示文本。 以下程序将更新 RadioButton 控件的 **“内容”** 属性。

::: moniker-end

### <a name="add-display-text-for-each-radio-button"></a>添加每个单选按钮的显示文本

1. 在 XAML 中将`HelloButton` 和 `GoodbyeButton` 的“内容”属性更新为 `"Hello"` 和 `"Goodbye"`。 XAML 标记现在应类似于以下示例：

   ```xaml
   <Grid>
        <TextBlock HorizontalAlignment="Left" Margin="252,47,0,0" TextWrapping="Wrap" Text="Select a message option and then choose the Display button." VerticalAlignment="Top"/>
        <RadioButton x:Name="HelloButton" Content="Hello" HorizontalAlignment="Left" Margin="297,161,0,0" VerticalAlignment="Top"/>
        <RadioButton x:Name="GoodbyeButton" Content="Goodbye" HorizontalAlignment="Left" Margin="488,161,0,0" VerticalAlignment="Top"/>
   </Grid>
   ```

### <a name="set-a-radio-button-to-be-checked-by-default"></a>设置要默认选中的单选按钮

这一步将设置要默认选中的 HelloButton，这样两个单选按钮中始终有一个处于选中状态。

1. 在 XAML 视图中，找到 HelloButton 的标记。

1. 添加 IsChecked 属性，并将其设置为“True”。 具体而言，添加 `IsChecked="True"`。

   XAML 标记现在应类似于以下示例：

   ```xaml
   <Grid>
        <TextBlock HorizontalAlignment="Left" Margin="252,47,0,0" TextWrapping="Wrap" Text="Select a message option and then choose the Display button." VerticalAlignment="Top"/>
        <RadioButton x:Name="HelloButton" Content="Hello" IsChecked="True" HorizontalAlignment="Left" Margin="297,161,0,0" VerticalAlignment="Top"/>
        <RadioButton x:Name="GoodbyeButton" Content="Goodbye" HorizontalAlignment="Left" Margin="488,161,0,0" VerticalAlignment="Top"/>
   </Grid>
   ```

最后添加的 UI 元素是 [Button](/dotnet/framework/wpf/controls/button) 控件。

### <a name="add-the-button-control"></a>添加按钮控件

::: moniker range="vs-2019"

1. 在“工具箱”中，找到“按钮”控件，然后通过将控件拖到设计视图的窗体中，将其添加到 RadioButton 控件下方的设计界面中。 如果使用的是 Visual Studio 2019 或更高版本，则会出现一条红线，帮助你使控件居中。

1. 在 XAML 视图中，将 Button 控件的“内容”值从 `Content="Button"` 更改为 `Content="Display"`，然后保存更改。

     你的窗口应与下图类似。

     ![包含控制标签的 Greetings 窗体](media/exploreide-greetingswithcontrollabels-cs.png "Greetings.xaml 的“设计”窗口的屏幕截图，其中显示了一个 TextBlock 控件、两个标有“Hello”和“Greeting”的 RadioButton 控件，以及一个标有“Display”的按钮。")

   XAML 标记现在应类似于以下示例：

   ```xaml
   <Grid>
        <TextBlock HorizontalAlignment="Left" Margin="252,47,0,0" TextWrapping="Wrap" Text="Select a message option and then choose the Display button." VerticalAlignment="Top"/>
        <RadioButton x:Name="HelloButton" Content="Hello" IsChecked="True" HorizontalAlignment="Left" Margin="297,161,0,0" VerticalAlignment="Top"/>
        <RadioButton x:Name="GoodbyeButton" Content="Goodbye" HorizontalAlignment="Left" Margin="488,161,0,0" VerticalAlignment="Top"/>
        <Button Content="Display" HorizontalAlignment="Left" Margin="377,270,0,0" VerticalAlignment="Top" Width="75"/>
   </Grid>
   ```

::: moniker-end

::: moniker range=">=vs-2022"

1. 在“工具箱”中，找到“按钮”控件，然后通过将控件拖到设计视图的窗体中，将其添加到 RadioButton 控件下方的设计界面中。 这些参考线可以帮助你将控件居中。

1. 在 XAML 视图中，将 Button 控件的“内容”值从 `Content="Button"` 更改为 `Content="Display"`，然后保存更改。

     你的窗口应类似于以下屏幕截图。

     :::image type="content" source="media/vs-2022/explore-ide-greetings-with-control-labels-cs.png" alt-text="Greetings.xaml 的“设计”窗口的屏幕截图，其中显示了一个 TextBlock 控件、两个标有“Hello”和“Greeting”的 RadioButton 控件，以及一个标有“Display”的按钮。":::

   XAML 标记现在应类似于以下示例：

   ```xaml
   <Grid>
        <TextBlock HorizontalAlignment="Left" Margin="252,47,0,0" TextWrapping="Wrap" Text="Select a message option and then choose the Display button." VerticalAlignment="Top"/>
        <RadioButton x:Name="HelloButton" Content="Hello" IsChecked="True" HorizontalAlignment="Left" Margin="297,161,0,0" VerticalAlignment="Top"/>
        <RadioButton x:Name="GoodbyeButton" Content="Goodbye" HorizontalAlignment="Left" Margin="488,161,0,0" VerticalAlignment="Top"/>
        <Button Content="Display" HorizontalAlignment="Left" Margin="377,270,0,0" VerticalAlignment="Top" Width="75"/>
   </Grid>
   ```

::: moniker-end

### <a name="add-code-to-the-display-button"></a>向显示按钮添加代码

::: moniker range="vs-2019"

此应用程序运行时，用户选择单选按钮，再选择“显示” 按钮之后，会显示一个消息框。 选择 Hello 将显示一个消息框，选择 Goodbye 将显示另一个。 若要创建此行为，请将代码添加到 Greetings.xaml.vb 中的 `Button_Click` 事件。

1. 在设计图面上，双击 **“显示”** 按钮。

     此时，“Greetings.xaml.cs”打开，光标位于 `Button_Click` 事件上。

    ```csharp
    private void Button_Click(object sender, RoutedEventArgs e)
    {

    }
    ```

1. 输入以下代码：

    ```csharp
    if (HelloButton.IsChecked == true)
    {
         MessageBox.Show("Hello.");
    }
    else if (GoodbyeButton.IsChecked == true)
    {
        MessageBox.Show("Goodbye.");
    }
    ```

1. 保存应用程序。

::: moniker-end

::: moniker range=">=vs-2022"

此应用程序运行时，用户选择单选按钮，再选择“显示” 按钮之后，会显示一个消息框。 选择 Hello 将显示一个消息框，选择 Goodbye 将显示另一个。 若要创建此行为，请将代码添加到 Greetings.xaml.vb 中的 `Button_Click` 事件。

1. 在设计图面上，双击 **“显示”** 按钮。

     此时，“Greetings.xaml.cs”打开，光标位于 `Button_Click` 事件上。

    ```csharp
    private void Button_Click(object sender, RoutedEventArgs e)
    {

    }
    ```

1. 输入以下代码：

    ```csharp
    if (HelloButton.IsChecked == true)
    {
         MessageBox.Show("Hello.");
    }
    else if (GoodbyeButton.IsChecked == true)
    {
        MessageBox.Show("Goodbye.");
    }
    ```

1. 保存应用程序。

::: moniker-end

## <a name="debug-and-test-the-application"></a>调试并测试应用程序

接下来将调试应用程序，查找错误并测试两个消息框是否正确显示。 下面的说明介绍如何生成和启动调试器，但以后可以阅读[生成 WPF 应用程序 (WPF)](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf) 和[调试 WPF](../../debugger/debugging-wpf.md) 获取有关详细信息。

### <a name="find-and-fix-errors"></a>查找并修复错误

在此步骤中，将遇到之前因更改 MainWindow.xaml 文件的名称而引起的错误。

#### <a name="start-debugging-and-find-the-error"></a>开始调试和查找错误

::: moniker range="vs-2019"

1. 通过按 F5或选择“调试”，然后选择“启动调试”，启动调试程序。

   将出现“中断模式”窗口，“输出”窗口指示发生 IOException :“找不到资源 'mainwindow.xaml'”。

   ![IOException 消息](../media/exploreide-ioexception.png "“输出”窗口的屏幕截图，其中显示了 System.IO.IOException 和消息“找不到资源 mainwindow.xaml”。")

1. 选择“调试”>“停止调试”以停止调试器 。

开始学习本教程时，我们将 MainWindow.xaml 重命名为 Greetings.xaml，但是该代码仍然引用 MainWindow.xaml 作为应用程序的启动 URI，因此该项目无法启动。

::: moniker-end

::: moniker range=">=vs-2022"

1. 通过按 F5或选择“调试”，然后选择“启动调试”，启动调试程序。

   将出现“中断模式”窗口，“输出”窗口指示发生 IOException :“找不到资源 'mainwindow.xaml'”。

   :::image type="content" source="media/vs-2022/explore-ide-ioexception.png" alt-text="“输出”窗口的屏幕截图，其中显示了 System.IO.IOException 和消息“找不到资源 mainwindow.xaml”。":::

1. 选择“调试”>“停止调试”以停止调试器 。

开始学习本教程时，我们将 MainWindow.xaml 重命名为 Greetings.xaml，但是该代码仍然引用 MainWindow.xaml 作为应用程序的启动 URI，因此该项目无法启动。

::: moniker-end
#### <a name="specify-greetingsxaml-as-the-startup-uri"></a>将 Greetings.xaml 指定为启动 URI

1. 在“解决方案资源管理器”中，打开“App.xaml”文件。

1. 将 `StartupUri="MainWindow.xaml"` 更改为 `StartupUri="Greetings.xaml"`，然后保存更改。

作为一个可选步骤，将应用程序窗口标题更改为匹配此新名称可以避免混淆。

1. 在“解决方案资源管理器”中，打开刚刚重命名的 Greetings.xaml 文件。

1. 将 Window.Title 属性的值从 `Title="MainWindow"` 更改为 `Title="Greetings"`，然后保存更改。

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

1. 打开“Greetings.xaml.cs”，并选择以下行：`MessageBox.Show("Hello.")`

1. 通过选择 **“调试”** -&gt; **“切换断点”** ，从菜单中添加断点。

     编辑器窗口最左侧边距中该代码行附近将显示一个红圈。

1. 选择以下行： `MessageBox.Show("Goodbye.")`。

1. 按“F9”键添加断点，然后按“F5”启动调试。

1. 在 **“Greetings”** 窗口中，选择 **“Hello”** 单选按钮，然后选择 **“显示”** 按钮。

    行 `MessageBox.Show("Hello.")` 将用黄色突出显示。 在 IDE 底部，“自动”、“本地”和“监视”窗口一起停靠在左侧，而“调用堆栈”、“断点”、“异常设置”、“命令”、“即时”和“输出”窗口一起停靠在右侧。

    ![调试程序中的断点](media/exploreide-debugbreakpoint.png "Visual Studio 中调试会话的屏幕截图。Greetings.xaml.cs 的代码窗口通过一根以黄色突出显示的线条显示执行已在断点处停止。")

1. 在菜单栏上，选择“调试”>“单步跳出” 。

     应用程序继续执行，并将显示出带有“Hello”的消息框。

1. 选择消息框上的 **“确定”** 按钮将其关闭。

1. 在 **“Greetings”** 窗口中，选择 **“Goodbye”** 单选按钮，然后选择 **“显示”** 按钮。

     行 `MessageBox.Show("Goodbye.")` 将用黄色突出显示。

1. 按“F5”键继续调试。 当消息框出现时，选择消息框上的 **“确定”** 按钮将其关闭。

1. 关闭应用程序窗口，停止调试。

1. 在菜单栏上，选择“调试”>“禁用所有断点” 。

::: moniker-end

::: moniker range=">=vs-2022"

1. 打开“Greetings.xaml.cs”，并选择以下行：`MessageBox.Show("Hello.")`

1. 通过选择 **“调试”** -&gt; **“切换断点”** ，从菜单中添加断点。

     编辑器窗口最左侧边距中该代码行附近将显示一个红圈。

1. 选择以下行： `MessageBox.Show("Goodbye.")`。

1. 按“F9”键添加断点，然后按“F5”启动调试。

1. 在 **“Greetings”** 窗口中，选择 **“Hello”** 单选按钮，然后选择 **“显示”** 按钮。
    
    行 `MessageBox.Show("Hello.")` 将用黄色突出显示。 在 IDE 底部，“自动”、“本地”和“监视”窗口一起停靠在左侧，而“调用堆栈”、“断点”、“异常设置”、“命令”、“即时”和“输出”窗口一起停靠在右侧。

    :::image type="content" source="media/vs-2022/explore-ide-debug-breakpoint.png" alt-text="Visual Studio 中调试会话的屏幕截图。Greetings.xaml.cs 的代码窗口通过一根以黄色突出显示的线条显示执行已在断点处停止。":::

1. 在菜单栏上，选择“调试”>“单步跳出” 。

     应用程序继续执行，并将显示出带有“Hello”的消息框。

1. 选择消息框上的 **“确定”** 按钮将其关闭。

1. 在 **“Greetings”** 窗口中，选择 **“Goodbye”** 单选按钮，然后选择 **“显示”** 按钮。

     行 `MessageBox.Show("Goodbye.")` 将用黄色突出显示。

1. 按“F5”键继续调试。 当消息框出现时，选择消息框上的 **“确定”** 按钮将其关闭。

1. 关闭应用程序窗口，停止调试。

1. 在菜单栏上，选择“调试”>“禁用所有断点” 。

::: moniker-end

### <a name="view-a-representation-of-the-ui-elements"></a>查看 UI 元素的表示形式

在正在运行的应用中，你会看到窗口顶部显示了一个小组件。 该小组件是一个运行时帮助程序，通过它可以快速访问一些有用的调试功能。 选择第一个按钮“转到实时可视化树”。 随即会看到一个包含一个树的窗口，树中包含页面的所有可视元素。 展开节点，找到你添加的按钮。

::: moniker range="vs-2019"
![实时可视化树窗口的屏幕截图](media/vs-2019/exploreide-live-visual-tree.png "“实时可视化树”窗口的屏幕截图，其中显示了正在运行的页面中的可视化元素树。")
::: moniker-end
::: moniker range=">=vs-2022"

:::image type="content" source="media/vs-2022/explore-ide-live-visual-tree.png" alt-text="“实时可视化树”窗口的屏幕截图，其中显示了正在运行的 HelloWPFApp.exe 中的可视化元素树。":::

::: moniker-end
### <a name="build-a-release-version-of-the-application"></a>生成应用程序的发布版本

确认一切就绪后，可以准备该应用程序的发布版本。

1. 在主菜单中，依次选择“生成” > “清理解决方案”，删除上一生成过程中创建的中间文件和输出文件。 此步骤不是必需的，但它可以清理调试生成输出。

1. 使用工具栏（当前显示“调试”）上的下拉列表控件把 HelloWPFApp 的生成配置从“调试”更改为“发布” 。

1. 选择“生成” > “生成解决方案”来生成解决方案 。

恭喜你完成本教程！ 可在解决方案和项目目录 (...\HelloWPFApp\HelloWPFApp\bin\Release) 下找到生成的 .exe 文件。

## <a name="next-steps"></a>后续步骤

恭喜你完成本教程！ 若要了解详情，请继续学习后续教程。

> [!div class="nextstepaction"]
> [继续学习更多 WPF 教程](/dotnet/framework/wpf/getting-started/wpf-walkthroughs/)

## <a name="see-also"></a>请参阅

- [工作效率提示](../../ide/productivity-features.md)
