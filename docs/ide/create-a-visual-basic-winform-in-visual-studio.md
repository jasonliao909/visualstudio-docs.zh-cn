---
title: 教程：使用 Visual Basic 创建 Windows 窗体应用
description: 在本教程中，了解如何使用 Visual Basic 在 Visual Studio 中创建 Windows 窗体应用。
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.topic: tutorial
ms.workload:
- multiple
dev_langs:
- VB
ms.date: 01/07/2022
ms.custom: vs-acquisition, get-started
ms.openlocfilehash: 86c0f162662c98383ba849db4ae78313143f8480
ms.sourcegitcommit: 7d319435c35075d4cec021b7b667666a81c02435
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2022
ms.locfileid: "137650461"
---
# <a name="tutorial-create-a-winforms-app-with-visual-basic"></a>教程：使用 Visual Basic 创建 WinForms 应用

在本教程中，你将创建一个具有 Windows 窗体用户界面的 Visual Basic 应用程序。
Visual Studio 集成开发环境 (IDE) 包含创建 Windows 窗体应用所需的所有工具。

在本教程中，你将了解如何执行以下操作：

> [!div class="checklist"]
> - 创建项目
> - 向窗体添加按钮
> - 添加标签和代码
> - 运行应用程序

## <a name="prerequisites"></a>先决条件

::: moniker range="vs-2017"
若要完成本教程，必须具有 Visual Studio。
请访问 [Visual Studio 下载页](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)获取免费版本。
::: moniker-end
::: moniker range="vs-2019"
若要完成本教程，必须具有 Visual Studio。
请访问 [Visual Studio 下载页](https://visualstudio.microsoft.com/vs/)获取免费版本。
::: moniker-end
::: moniker range=">=vs-2022"
若要完成本教程，必须具有 Visual Studio。
请访问 [Visual Studio 下载页](https://visualstudio.microsoft.com/downloads)获取免费版本。
::: moniker-end

## <a name="create-a-project"></a>创建项目

创建 Visual Basic 应用程序项目。
项目类型随附了所需的全部模板文件，无需添加任何内容。

::: moniker range="vs-2017"
1. 打开 Visual Studio 2017。

1. 在顶部菜单中，选择 "**文件**" " > **新建** > **Project**"。

1. 在左侧窗格的 "**新建 Project** " 对话框中，展开 " **Visual Basic**"，然后选择 " **Windows 桌面**"。
   在中间窗格中，选择 " **Windows 窗体应用 (.NET Framework")**"。 随后将文件命名为 `HelloWorldApp`。

   ![屏幕截图显示在 Visual Studio 安装程序中选择的 .net Core 工作负荷。](../ide/media/install-dot-net-desktop-env.png)

   > [!NOTE]
   > 如果看不到 " **Windows 窗体应用" (.NET Framework)** 项目模板，则取消 "**新建 Project** " 对话框。
   > 选择 "**工具**" "  >  **获取工具和功能**"。
   > Visual Studio 安装程序启动。
   > 选择 " **.net 桌面开发** " 工作负载，然后选择 " **修改**"。

::: moniker-end

::: moniker range="vs-2019"
1. 打开 Visual Studio。

1. 在“开始”窗口上，选择“创建新项目”  。

   ![屏幕截图显示了 "创建新项目" Visual Studio 2019 的 "开始" 窗口。](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. 在 "**创建新项目**" 窗口中，选择 " **Windows 窗体应用" (.NET Framework** Visual Basic 的) 模板。

   你可以优化搜索，迅速获取所需的模板。
   例如，在 "搜索" 框中输入 *Windows 窗体应用*。
   接下来，从 "**语言**" 列表中选择 " **Visual Basic** "，然后从 "**平台**" 列表中 **Windows** 。  

   ![屏幕截图显示 "新建项目" 窗口，该窗口中 Windows 窗体应用 (.NET Framework) 处于选中状态。](../get-started/visual-basic/media/vs-2019/vb-create-new-project-search-winforms-filtered.png)

   > [!NOTE]
   > 如果未看到“Windows 窗体应用(.NET Framework)”模板，则可以通过“创建新项目”窗口安装该模板。
   > 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > ![屏幕截图显示了 "从找不到要查找的内容" 消息中的 "安装更多工具和功能" 链接。](../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > 接下来，在 Visual Studio 安装程序中，选择“.NET 桌面开发”工作负载。
   >
   > ![屏幕截图显示在 Visual Studio 安装程序中选择的 .net Core 工作负荷。](../ide/media/install-dot-net-desktop-env.png)
   >
   > 然后，在 Visual Studio 安装程序中选择 "**修改**"。 系统可能会提示你保存工作内容。

1. 在 "**配置新项目**" 窗口中，输入 " *HelloWorld* " 作为 **Project 名称**。 然后选择“创建”。

   ![屏幕截图显示 "配置新项目" 窗口，并输入名称 HelloWorld。](../get-started/visual-basic/media/vs-2019/vb-name-your-winform-project-helloworld.png)

   此时，Visual Studio 将打开新项目。

::: moniker-end

::: moniker range=">=vs-2022"
1. 打开 Visual Studio。

1. 在“开始”窗口上，选择“创建新项目”  。

   ![屏幕截图显示了 "创建新项目" Visual Studio 2022 的 "开始" 窗口。](../get-started/media/vs-2022/create-new-project.png)

1. 在 "**创建新项目**" 窗口中，选择 " **Windows 窗体应用" (.NET Framework** Visual Basic 的) 模板。

   你可以优化搜索，迅速获取所需的模板。
   例如，在 "搜索" 框中输入 *Windows 窗体应用*。
   接下来，从 "**语言**" 列表中选择 " **Visual Basic** "，然后从 "**平台**" 列表中 **Windows** 。  

   ![屏幕截图显示 "新建项目" 窗口，该窗口中 Windows 窗体应用 (.NET Framework) 处于选中状态。](../get-started/visual-basic/media/vs-2019/vb-create-new-project-search-winforms-filtered.png)

   > [!NOTE]
   > 如果未看到“Windows 窗体应用(.NET Framework)”模板，则可以通过“创建新项目”窗口安装该模板。
   > 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > ![屏幕截图显示了 "从找不到要查找的内容" 消息中的 "安装更多工具和功能" 链接。](../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > 接下来，在 Visual Studio 安装程序中，选择“.NET 桌面开发”工作负载。
   >
   > ![屏幕截图显示在 Visual Studio 安装程序中选择的 .net Core 工作负荷。](../ide/media/install-dot-net-desktop-env.png)
   >
   > 然后，在 Visual Studio 安装程序中选择 "**修改**"。 系统可能会提示你保存工作内容。

1. 在 "**配置新项目**" 窗口中，输入 " *HelloWorld* " 作为 **Project 名称**。 然后选择“创建”。

   ![屏幕截图显示 "配置新项目" 窗口，并输入名称 HelloWorld。](../get-started/visual-basic/media/vs-2019/vb-name-your-winform-project-helloworld.png)

   此时，Visual Studio 将打开新项目。

::: moniker-end

## <a name="add-a-button-to-the-form"></a>向窗体添加按钮

选择 Visual Basic 项目模板并为文件命名后，Visual Studio 会打开一个窗体。
窗体就是 Windows 用户界面。
您将通过向窗体添加控件来创建 "Hello World" 应用程序。

1. 在 Visual Studio IDE 的左侧，选择“工具箱”选项卡。如果没有看到，则从菜单栏中选择“查看”>“工具箱”或者按 Ctrl+Alt+X 键     。

   ![屏幕截图显示了打开工具箱窗口的 "工具箱" 选项卡。](media/create-a-visual-basic-winform-in-visual-studio/toolbox-tab.png)

   如果需要，请选择 **固定** 图标来停靠 " **工具箱** " 窗口。

1. 选择“按钮”控件，然后将其拖到窗体上。

   ![屏幕截图显示添加到窗体的按钮控件。](media/create-a-visual-basic-winform-in-visual-studio/toolbox-button-form.png)

1. 在 "**属性**" 窗口的 "**外观**" 部分，键入 "**文本** *"，再* 按 **enter**。

   ![屏幕截图显示具有值的文本属性单击此。](media/create-a-visual-basic-winform-in-visual-studio/button-text-property.png)

   如果看不到 " **属性** " 窗口，可从菜单栏打开它。 选择 "**查看**  >  **属性" 窗口** 或按 **F4**。

1. 在 "**属性**" 窗口的 "**设计**" 部分，将名称从 **Button1** 更改为 *btnClickThis*，然后按 **enter**。

   ![屏幕截图显示名称属性，其值为 b t n 单击此。](media/create-a-visual-basic-winform-in-visual-studio/button-name-property.png)

   > [!NOTE]
   > 如果按字母顺序排列了“属性”  窗口列表，则 Button1  会显示在 (DataBindings)  部分中。

## <a name="add-a-label-and-code"></a>添加标签和代码

现在，您已添加了一个按钮控件用于创建操作，接下来请添加一个用于发送文本的 "标签" 控件。

1. 选择 "**工具箱**" 窗口中的 "**标签**" 控件，然后将其拖到窗体上。
   将其置于 " **单击此** 按钮" 下。

1. 在 "**属性**" 窗口的 "**设计**" 部分或 " **(** databinding") 部分中，将名称 **Label1** 更改为 *lblHelloWorld*，然后按 **enter**。

1. 在“Form1.vb [设计]”窗口中，双击“单击此处”按钮，打开“Form1.vb”窗口。

   另一种方法是在 **解决方案资源管理器** 中展开 " **form1** "，然后选择 " **form1**"。

1. 在 " **Form1** " 窗口的 " **专用 sub** " 和 " **结束" 子** 行之间，输入 *lblHelloWorld = "Hello World！"* 如以下屏幕截图所示：

     ![屏幕截图显示了 "Form1. vs" 选项卡中的一个类，你可以在其中添加 Visual Basic 代码。](media/create-a-visual-basic-winform-in-visual-studio/click-handle-code-visual-basic.png)

## <a name="run-the-application"></a>运行应用程序

你的应用程序已准备就绪，可以生成并运行。

1. 选择 " **启动** " 以运行应用程序。

   ![屏幕截图显示运行你的应用程序的 "开始" 按钮。](media/create-a-visual-basic-winform-in-visual-studio/visual-studio-start-debug.png)

   发生了几种情况。
   在 Visual Studio IDE 中，将打开 "**诊断工具**" 窗口，并打开 "**输出**" 窗口。
   在 IDE 外部，会出现一个 " **Form1** " 对话框。
   它包括您 **单击此** 按钮和显示 " **Label1**" 的文本。

1. 选择“Form1”对话框中的“单击此处”按钮 。

   ![屏幕截图显示标题为 "窗体 1" 的对话框，其中显示文本 Hello World！](media/create-a-visual-basic-winform-in-visual-studio/visual-studio-dialog-hello-world.png)

   **Label1** 文本更改为 **Hello World！**。

1. 关闭“Form1”  对话框以停止运行应用。

## <a name="next-steps"></a>后续步骤

若要详细了解 Windows 窗体，请继续学习以下教程：

> [!div class="nextstepaction"]
> [教程：创建图片查看器](tutorial-windows-forms-picture-viewer-layout.md)

## <a name="see-also"></a>请参阅

* [更多 Visual Basic 教程](../get-started/visual-basic/index.yml)
* [C# 教程](../get-started/csharp/index.yml)
* [C++ 教程](/cpp/get-started/tutorial-console-cpp)
