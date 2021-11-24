---
title: 教程：使用 Visual Studio 创建 C# 控制台应用
titleSuffix: ''
description: 了解如何在 Visual Studio 中使用 C# 逐步创建简单的 Hello World 控制台应用。
ms.custom: vs-acquisition
ms.date: 09/14/2021
ms.topic: quickstart
ms.devlang: vb
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: ca9dbaba1ddb1ea94e801c497aa3c6d3176b7c1b
ms.sourcegitcommit: 932cf0f653c6258b73f42102d134cbaf50b8f20c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2021
ms.locfileid: "132880046"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-c-console-app"></a>快速入门：使用 Visual Studio 创建第一个 C# 控制台应用

在这个 5-10 分钟的 Visual Studio 集成开发环境 (IDE) 简介中，你将了解如何创建在控制台上运行的简单 C# 应用。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range=">=vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

## <a name="create-a-project"></a>创建项目

首先，创建 C# 应用程序项目。 项目类型随附了所需的全部模板文件，无需添加任何内容！

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

1. 从顶部菜单栏中选择“文件”>“新建”>“项目”    。

1. 在“新建项目”  对话框的左窗格中，展开“C#”  ，然后选择“.NET Core”  。 在中间窗格中，选择“控制台应用(.NET Core)”  。 随后将项目命名为 HelloWorld。

   ![Visual Studio IDE 中“新建项目”对话框中的控制台应用 (.NET Core) 项目模板的屏幕截图。](../ide/media/new-project-csharp-dotnetcore-helloworld-console-app.png)

     如果看不到“控制台应用(.NET Core)”  项目模板，请选择“新建项目”  对话框左侧窗格中的“打开 Visual Studio 安装程序”  链接。

   ![“新建项目”对话框中的“打开 Visual Studio 安装程序”链接的屏幕截图。](../ide/media/csharp-open-visual-studio-installer-hello-world.png)

     Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改” 。

     ![Visual Studio 安装程序中的“.NET Core 跨平台开发”工作负载的屏幕截图。](../ide/media/dot-net-core-xplat-dev-workload.png)

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio。

1. 在“开始”窗口上，选择“创建新项目”  。

   ![“创建新项目”窗口的屏幕截图。](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. 在“创建新项目”窗口的搜索框中输入或键入“控制台”   。 接下来，从“语言”列表中选择 C#，然后从“平台”列表中选择 Windows 。 

   应用语言和平台筛选器之后，选择“控制台应用(.NET Core)”模板，然后选择“下一步” 。

   ![控制台应用 (.NET Framework) 的 C# 模板的屏幕截图。](../get-started/csharp/media/vs-2019/csharp-create-new-project-search-console-net-core-filtered.png)

   > [!NOTE]
   > 如果未看到“控制台应用(.NET Core)”模板，则可以通过“创建新项目”窗口安装该模板 。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > ![“创建新项目”窗口内“找不到所需内容”消息中的“安装更多工具和功能”链接的屏幕截图。](../get-started/media/vs-2019/not-finding-what-looking-for.png) 
   > 
   > 然后，在 Visual Studio 安装程序中，选择“.NET Core 跨平台开发”工作负载  。
   >
   > ![Visual Studio 安装程序中的“.NET Core 跨平台开发”工作负载的屏幕截图。](./media/dot-net-core-xplat-dev-workload.png)
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 系统可能会提示你保存所有内容；如果出现提示，请按照指示进行操作。 接下来，选择“继续”，以安装工作负载  。 然后，返回到“[创建项目](#create-a-project)”过程中的步骤 2。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“HelloWorld”    。 然后，选择“创建”  。

   ![“配置新项目”窗口的屏幕截图，项目命名为“HelloWorld”。](../get-started/csharp/media/vs-2019/csharp-name-your-helloworld-project.png)

   此时，Visual Studio 将打开新项目。

::: moniker-end

::: moniker range=">=vs-2022"

1. 打开 Visual Studio。

1. 在“开始”窗口上，选择“创建新项目”  。

   ![Visual Studio 2022 中“创建新项目”窗口的屏幕截图。](media/vs-2022/start-window-create-new-project.png)

1. 在“创建新项目”窗口的搜索框中输入或键入“控制台”   。 接下来，从“语言”列表中选择 C#，然后从“平台”列表中选择 Windows 。 

   应用语言和平台筛选器之后，选择“控制台应用程序”模板，然后选择“下一步” 。

   ![控制台应用 (.NET Core) 的 C# 模板的屏幕截图。](media/vs-2022/quickstart-csharp-create-new-project.png)

   > [!NOTE]
   > 如果没有看到 .NET Core 的“控制台应用程序”模板，可以从“创建新项目”窗口安装此模板： 
   > - 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接 以启动 Visual Studio 安装程序。
   >
   >    ![“创建新项目”窗口内“找不到所需内容”消息中的“安装更多工具和功能”链接的屏幕截图。](media/vs-2022/not-finding-what-looking-for.png)
   > 
   > - 在 Visual Studio 安装程序中：
   >   - 选择“.NET 桌面开发”工作负载。
   >
   >      ![Visual Studio 安装程序中的“.NET Core 跨平台开发”工作负载的屏幕截图。](media/vs-2022/dot-net-core-desktop-dev-workload.png)
   >
   >   - 选择“修改”按钮。 系统可能会提示你保存所有内容；如果出现提示，请按照指示进行操作。 
   >   - 选择“继续”，以安装工作负载。
   > - 返回到“[创建项目](#create-a-project)”过程中的步骤 2。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“HelloWorld”    。 然后，选择“下一步”。

   ![Visual Studio 2022 中“配置新项目”窗口的屏幕截图，项目名称设置为“HelloWorld”。](media/vs-2022/csharp-name-your-helloworld-project.png)

1. 在“其他信息”窗口中，确保在“框架”下拉菜单中选择“.NET 6.0”，然后选择“创建”   。

   ![Visual Studio 2022 中的“其他信息”窗口的屏幕截图，其中“Framework”设置为“.NET 6.0”。](media/vs-2022/create-project-additional-info.png)

   此时，Visual Studio 将打开新项目。
   
::: moniker-end

## <a name="create-the-application"></a>创建应用程序

::: moniker range="vs-2017"

选择 C# 项目模板并为项目命名后，Visual Studio 会创建一个简单的“Hello World”应用程序。

::: moniker-end

::: moniker range="vs-2019"

Visual Studio 在项目中包含默认的“Hello World”代码。

::: moniker-end

::: moniker range=">=vs-2022"

Visual Studio 在项目中包含默认的“Hello World”代码。 如果要在编辑器中查看它，可以在“解决方案资源管理器”窗口中选择代码文件“Program.cs”，该窗口通常位于 Visual Studio 的右侧。

::: moniker-end

::: moniker range="<=vs-2019"

（为此，它通过调用 <xref:System.Console.WriteLine%2A> 方法在控制台窗口中 显示文本字符串“Hello World!”。）

   ![模板中的默认 Hello World 代码的屏幕截图。](../ide/media/csharp-console-helloworld-template.png)

如果按 F5，可以在调试模式下运行程序。 但是，控制台窗口短暂出现后就会关闭。

（此行为是因为 `Main` 方法在执行其单个语句后就会终止，应用程序因而结束。）

::: moniker-end

::: moniker range=">=vs-2022"

单个代码语句调用 <xref:System.Console.WriteLine%2A> 方法显示文本字符串“Hello World!” 显示文本字符串“Hello World!”。

   ![模板中的默认 Hello World 代码的屏幕截图。](media/vs-2022/csharp-console-helloworld-template.png)

如果按 F5，可以在调试模式下运行程序。 在调试器中运行应用程序后，控制台窗口将保持打开状态。 但是，如果应用程序在调试器外部运行，则控制台窗口仅在关闭之前的一段时间内可见。 这是因为 `Main` 方法在执行其单个代码语句后就会终止，应用程序因而结束。 有关在调试器外部运行控制台应用程序的详细信息，请参阅[发布 .NET 控制台应用程序](/dotnet/core/tutorials/publishing-with-visual-studio)。

> [!NOTE]
> 编辑器中的单个代码行是一个 C# [顶级语句](/dotnet/csharp/whats-new/csharp-9#top-level-statements)，并且是样板 [Main](/dotnet/csharp/fundamentals/program-structure/main-command-line) 方法的简化形式。

::: moniker-end

### <a name="add-some-code"></a>添加一些代码

::: moniker range="<=vs-2019"

让我们添加一些代码来暂停应用程序，以便控制台窗口不会关闭，直到你按下 ENTER。

1. 在 <xref:System.Console.WriteLine%2A> 方法调用后面紧接着添加以下代码：

   ```csharp
   Console.ReadLine();
   ```

1. 验证其外观在代码编辑器中如下所示：

   ![用于暂停 Hello World 应用的新添加代码的屏幕截图。](../ide/media/csharp-console-helloworld-add-code.png)

::: moniker-end

::: moniker range=">=vs-2022"

让我们添加一些代码来暂停应用程序，使 `main` 方法在你按下 ENTER 前不会终止。

1. 在 <xref:System.Console.WriteLine%2A> 方法调用后面紧接着添加以下代码：

   ```csharp
   Console.ReadLine();
   ```

1. 验证其外观在代码编辑器中如下所示：

   ![用于暂停 Hello World 应用的新添加代码的屏幕截图。](media/vs-2022/csharp-console-helloworld-add-code.png)

::: moniker-end

## <a name="run-the-application"></a>运行应用程序

::: moniker range="<=vs-2019"

1. 选择工具栏中的“HelloWorld”按钮，在调试模式下运行应用程序。 或者，可以按 F5。

   ![从工具栏运行应用的“Hello World”按钮的屏幕截图。](../ide/media/csharp-console-hello-world-button.png)

1. 在控制台窗口中查看你的应用。

   ![显示“Hello World!”的控制台窗口的屏幕截图 消息作为响应。](../ide/media/csharp-console-hello-world.png)

::: moniker-end

::: moniker range=">=vs-2022"

1. 选择工具栏中的“HelloWorld”按钮，在调试模式下运行应用程序。 （或者，可以按 F5。）

   ![从工具栏运行应用的“Hello World”按钮的屏幕截图。](media/vs-2022/csharp-console-hello-world-button.png)

1. 在控制台窗口中查看你的应用。

   ![显示“Hello, World!”的控制台窗口的屏幕截图 消息作为响应。](media/vs-2022/csharp-console-hello-world.png)

::: moniker-end

### <a name="close-the-application"></a>关闭该应用程序

::: moniker range="<=vs-2019"

1. 按 ENTER 关闭控制台窗口。

1. 关闭 Visual Studio 中的输出窗格。

   ![Visual Studio 中“输出”窗格的屏幕截图。](../ide/media/csharp-hello-world-close-output-pane.png)

1. 关闭 Visual Studio。

::: moniker-end

::: moniker range=">=vs-2022"

1. 按 ENTER 终止 `main` 方法，然后再次按 ENTER 关闭控制台窗口。

1. 关闭 Visual Studio 中的输出窗格。

   ![Visual Studio 2022 中“输出”窗格的屏幕截图。](media/vs-2022/csharp-hello-world-close-output-pane.png)

1. 关闭 Visual Studio。

::: moniker-end

## <a name="next-steps"></a>后续步骤

祝贺你完成此快速入门！ 我们希望你已对 C# 和 Visual Studio IDE 有了一定了解。 要更加深入地了解，请继续学习下面的教程。

> [!div class="nextstepaction"]
> [Visual Studio 中的 C# 控制台应用程序入门](../get-started/csharp/tutorial-console.md)
