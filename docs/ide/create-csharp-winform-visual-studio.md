---
title: 使用 C# 创建 Windows 窗体应用
description: 了解如何在 Visual Studio 中使用 C# 分步创建 Windows 窗体应用。
ms.custom: vs-acquisition, get-started
ms.date: 11/08/2021
ms.topic: tutorial
ms.devlang: CSharp
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: b323df635e3b338853ef5be2501466d68ba6168e
ms.sourcegitcommit: 7d319435c35075d4cec021b7b667666a81c02435
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2022
ms.locfileid: "137650460"
---
# <a name="create-a-windows-forms-app-in-visual-studio-with-c"></a>在 Visual Studio 中使用 C\# 创建 Windows 窗体应用

在此 Visual Studio 集成开发环境 (IDE) 简介中，了解如何创建具有基于 Windows 的用户界面 (UI) 的简单 C# 应用程序。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

> [!NOTE]
> 本教程中的部分屏幕截图使用深色主题。 如果没有深色主题但想要使用，请参阅[个性化设置 Visual Studio IDE 和编辑器](../ide/quickstart-personalize-the-ide.md)页面，了解具体方法。

::: moniker-end

::: moniker range="vs-2022"

如果尚未安装 Visual Studio，请转到 [Visual Studio 2022 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

## <a name="create-a-project"></a>创建项目

首先，创建 C# 应用程序项目。 项目类型随附了所需的全部模板文件，无需添加任何内容。

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

1. 从顶部菜单栏中选择“文件”>“新建”>“项目”    。

1. 在“新建项目”  对话框左侧的窗格中，展开“Visual C#”  ，然后选择“Windows 桌面”  。 在中间窗格中，选择“Windows 窗体应用(.NET Framework)”  。 随后将文件命名为 `HelloWorld`。

     如果没有看到“Windows 窗体应用(.NET Framework)”  项目模板，则取消“新建项目”  对话框，然后在顶部菜单栏中依次选择“工具”   > “获取工具和功能”  。 Visual Studio 安装程序启动。 选择“.NET 桌面开发”工作负载，然后选择“修改”   。

     ![Visual Studio 安装程序中的 .NET Core 开发工作负载](../ide/media/install-dot-net-desktop-env.png)

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio。

1. 在“开始”窗口上，选择“创建新项目”  。

   ![查看“创建新项目”窗口](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. 在“创建新项目”  窗口中，为 C# 选择“Windows 窗体应用(.NET Framework)”  模板。

   如果愿意，你可以优化搜索以快速找到所需的模板。 例如，在搜索框中输入或键入“Windows 窗体应用”  。 接下来，从“语言”列表中选择“C#”  ，然后从“平台”列表中选择“Windows”  。）  

   ![为 Windows 窗体应用 (.NET Framework) 选择 C# 模板](../get-started/csharp/media/vs-2019/csharp-create-new-winforms-project-nonfiltered.png)

   > [!NOTE]
   > 如果未看到“Windows 窗体应用(.NET Framework)”  模板，则可以通过“创建新项目”  窗口安装该模板。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > ![“创建新项目”窗口内“找不到所需内容”消息中的“安装更多工具和功能”链接](../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > 接下来，在 Visual Studio 安装程序中，选择“.NET 桌面开发”工作负载。
   >
   > ![Visual Studio 安装程序中的 .NET Core 开发工作负载](../ide/media/install-dot-net-desktop-env.png)
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 系统可能会提示你保存所有内容；如果出现提示，请按照指示进行操作。 接下来，选择“继续”，以安装工作负载  。 然后，返回到“[创建项目](#create-a-project)”过程中的步骤 2。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“HelloWorld”    。 然后，选择“创建”  。

   ![在“配置新项目”窗口中，将项目命名为“HelloWorld”](../get-started/csharp/media/vs-2019/csharp-name-your-winform-project-helloworld.png)

   此时，Visual Studio 将打开新项目。

::: moniker-end

::: moniker range=">=vs-2022"

1. 打开 Visual Studio。

1. 在“开始”窗口中，选择“创建新项目”。
    
    :::image type="content" source="media/vs-2022/create-new-project-dark-theme.png" alt-text="显示“创建新项目”窗口的屏幕截图。":::

1. 在“创建新项目”窗口中，为 C# 选择“Windows 窗体应用(.NET Framework)”模板 。

   如果愿意，你可以优化搜索以快速找到所需的模板。 例如，在搜索框中输入或键入“Windows 窗体应用”  。 接下来，从语言列表中选择“C#”，然后从平台列表中选择“Windows” 。  

    :::image type="content" source="media/vs-2022/csharp-winform-create-a-new-project.png" alt-text="显示为 Windows 窗体应用 (.NET Framework) 选择 C# 模板的屏幕截图。":::

   > [!NOTE]
   > 如果未看到“Windows 窗体应用(.NET Framework)”  模板，则可以通过“创建新项目”  窗口安装该模板。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接 。
   >
   > :::image type="content" source="../get-started/media/vs-2019/not-finding-what-looking-for.png" alt-text="显示“创建新项目”窗口内“找不到所需内容”消息中的“安装更多工具和功能”链接的屏幕截图。":::
   >
   > 接下来，在 Visual Studio 安装程序中，选择“.NET 桌面开发”工作负载。
   >
   > :::image type="content" source="media/vs-2022/install-dot-net-desktop-env.png" alt-text="显示 Visual Studio 安装程序中的 .NET Core 工作负载的屏幕截图。":::
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮。 系统可能会提示你保存所有内容；如果出现提示，请按照指示进行操作。 接下来，选择“继续”以安装工作负载。 然后，返回到“[创建项目](#create-a-project)”过程中的步骤 2。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“HelloWorld”    。 然后选择“创建”。

    :::image type="content" source="media/vs-2022/csharp-winform-configure-new-project.png" alt-text="显示“配置新项目”窗口和将项目命名为“HelloWorld”的屏幕截图":::

   此时，Visual Studio 将打开新项目。

## <a name="create-the-application"></a>创建应用程序

选择 C# 项目模板并为文件命名后，Visual Studio 会打开一个窗体。 窗体就是 Windows 用户界面。 通过向窗体添加控件创建“Hello World”应用程序，然后运行该应用程序。

### <a name="add-a-button-to-the-form"></a>向窗体添加按钮

1. 选择“工具箱”，打开“工具箱”弹出窗口。
    
     :::image type="content" source="media/vs-2022/csharp-winform-hello-world-project-toolbox.png" alt-text="选择“工具箱”以打开“工具箱”窗口的屏幕截图。":::

     （如果看不到“工具箱”弹出选项，可从菜单栏打开  。 为此，请选择“视图”   > “工具箱”  。 或按 Ctrl+Alt+X。）   

1. 选择“固定”图标，固定“工具箱”窗口 。

     :::image type="content" source="media/vs-2022/csharp-winform-toolbox-flyout-pin.png" alt-text="显示选择“固定”图标来将“工具箱”窗口固定到 IDE 的屏幕截图。":::

1. 选择“按钮”控件，然后将其拖到窗体上。

     :::image type="content" source="media/vs-2022/csharp-winform-add-button-on-form.png" alt-text="向窗体添加按钮的屏幕截图。":::

1. 在属性窗口中，找到“文本”，将名称从“Button1”更改为 `Click this`然后按 Enter   。

     :::image type="content" source="media/vs-2022/csharp-winform-button-properties-text.png" alt-text="使用属性窗口将文本添加到窗体上的按钮的屏幕截图。":::

     （如果看不到“属性”窗口，可从菜单栏打开  。 为此，请选择“视图” > “属性窗口” 。 或按 F4。） 

1. 在属性窗口的“设计”部分，将名称从“Button1”更改为 `btnClickThis`，然后按 Enter   。

     :::image type="content" source="media/vs-2022/csharp-winform-button-properties-design-name.png" alt-text="使用属性窗口将函数添加到窗体上的按钮的屏幕截图。":::

   > [!NOTE]
   > 如果按字母顺序排列了属性窗口列表，则 button1 会显示在 (DataBindings) 部分中  。

### <a name="add-a-label-to-the-form"></a>向窗体添加标签

添加创建操作的按钮控件后，我们来添加发送文本的标签控件。

1. 从“工具箱”窗口选择“标签”控件，然后将其拖到窗体上，并放到“单击此处”按钮下方    。

1. 在属性窗口的“设计”部分或“(DataBindings)”部分，将 label1 的名称更改为 `lblHelloWorld`，然后按 Enter    。

### <a name="add-code-to-the-form"></a>向窗体添加代码

1. 在“Form1.cs &#91;设计&#93;”  窗口中，双击“单击此处”  按钮，打开“Form1.cs”窗口  。

      （或者，可在“解决方案资源管理器”  中展开“Form1.cs”  ，然后选择“Form1”  。）

1. 在“Form1.cs”  窗口中，在“private void”  行后，键入或输入 `lblHelloWorld.Text = "Hello World!";`，如以下屏幕截图所示：

     :::image type="content" source="media/vs-2022/csharp-winform-button-click-code.png" alt-text="向窗体添加代码的屏幕截图":::

## <a name="run-the-application"></a>运行应用程序

1. 选择“启动”按钮运行应用程序。

     :::image type="content" source="media/vs-2022/csharp-winform-visual-studio-start-run-program.png" alt-text="选择“启动”来调试和运行应用的屏幕截图。":::

   将出现以下几种情况。 在 Visual Studio IDE 中，“诊断工具”窗口打开，同时还会打开一个“输出”窗口   。 在 IDE 外部，会出现一个“Form1”对话框  。 其中包含“单击此处”按钮和显示“label1”的文本 。

1. 选择“Form1”对话框中的“单击此处”按钮 。 请注意，“label1”文本会更改为“Hello World!” 。

     :::image type="content" source="media/vs-2022/csharp-winform-form.png" alt-text="显示包含 label1 文本的“Form1”对话框的屏幕截图。":::

1. 关闭“Form1”  对话框以停止运行应用。

::: moniker-end

::: moniker range="<=vs-2019"
## <a name="create-the-application"></a>创建应用程序

选择 C# 项目模板并为文件命名后，Visual Studio 会打开一个窗体。 窗体就是 Windows 用户界面。 通过向窗体添加控件创建“Hello World”应用程序，然后运行该应用程序。

### <a name="add-a-button-to-the-form"></a>向窗体添加按钮

1. 选择“工具箱”，打开“工具箱”弹出窗口  。

     ![选择“工具箱”，打开“工具箱”窗口](../ide/media/csharp-toolbox-toolwindow.png)

     （如果看不到“工具箱”弹出选项，可从菜单栏打开  。 为此，请选择“视图”   > “工具箱”  。 或按 Ctrl+Alt+X。）   

1. 选择“固定”  图标，固定“工具箱”  窗口。

     ![选择“固定”图标，将“工具箱”窗口固定到 IDE](../ide/media/vb-pin-the-toolbox-window.png)

1. 选择“按钮”  控件，然后将其拖到窗体上。

     ![向窗体添加按钮](../ide/media/csharp-add-button-form1.png)

1. 在“属性”  窗口中，找到“文本”  ，将名称从“Button1”  更改为 `Click this`然后按 Enter  。

     ![向窗体上的按钮添加文本](../ide/media/vb-button-control-text.png)

     （如果看不到“属性”窗口，可从菜单栏打开  。 若要执行此操作，请选择“视图”   > “属性窗口”  。 或按 F4。） 

1. 在“属性”窗口的“设计”部分，将名称从“Button1”更改为 `btnClickThis`，然后按 Enter     。

     ![向窗体上的按钮添加功能](../ide/media/vb-button-control-function.png)

   > [!NOTE]
   > 如果按字母顺序排列了“属性”  窗口列表，则 Button1  会显示在 (DataBindings)  部分中。

### <a name="add-a-label-to-the-form"></a>向窗体添加标签

添加创建操作的按钮控件后，我们来添加发送文本的标签控件。

1. 从“工具箱”窗口选择“标签”控件，然后将其拖到窗体上，并放到“单击此处”按钮下方    。

1. 在“属性”  窗口的“设计”  部分或“(DataBindings)”  部分，将“Label1”  的名称更改为 `lblHelloWorld`，然后按 Enter  。

### <a name="add-code-to-the-form"></a>向窗体添加代码

1. 在“Form1.cs &#91;设计&#93;”  窗口中，双击“单击此处”  按钮，打开“Form1.cs”窗口  。

      （或者，可在“解决方案资源管理器”  中展开“Form1.cs”  ，然后选择“Form1”  。）

1. 在“Form1.cs”  窗口中，在“private void”  行后，键入或输入 `lblHelloWorld.Text = "Hello World!";`，如以下屏幕截图所示：

     ![向窗体添加代码](../get-started/csharp/media/csharp-winforms-add-code.png)

## <a name="run-the-application"></a>运行此应用程序

1. 选择“启动”  按钮运行应用程序。

     ![选择“启动”，调试和运行应用](../ide/media/vb-click-start-hello-world.png)

   将出现以下几种情况。 在 Visual Studio IDE 中，“诊断工具”窗口打开，同时还会打开一个“输出”窗口   。 在 IDE 外部，会出现一个“Form1”对话框  。 其中包含“单击此处”按钮和显示“Label1”的文本   。

1. 选择“Form1”  对话框中的“单击此处”  按钮。 请注意，“Label1”文本会更改为“Hello World!”   。

    ![包含 Label1 文本的“Form1”对话框 ](../ide/media/vb-form1-dialog-hello-world.png)

1. 关闭“Form1”  对话框以停止运行应用。

::: moniker-end

## <a name="next-steps"></a>后续步骤

要更加深入地了解，请继续学习下面的教程：

> [!div class="nextstepaction"]
> [教程：创建图片查看器](tutorial-windows-forms-picture-viewer-layout.md)

## <a name="see-also"></a>请参阅

* [更多 C# 教程](../get-started/csharp/index.yml)
* [Visual Basic 教程](../get-started/visual-basic/index.yml)
* [C++ 教程](/cpp/get-started/tutorial-console-cpp)