---
title: 使用 Visual Basic 创建首个控制台应用
description: 了解如何在 Visual Studio 中使用 Visual Basic 逐步创建简单的 Hello World 控制台应用。
ms.custom: vs-acquisition
ms.date: 09/14/2021
ms.topic: quickstart
ms.devlang: vb
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- vb
ms.workload:
- multiple
ms.openlocfilehash: 0ece22de8280742a099432fd5b3e527631718cfb
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128427793"
---
# <a name="quickstart-create-your-first-console-app-in-visual-studio-with-visual-basic"></a>快速入门：使用 Visual Basic 在 Visual Studio 中创建第一个控制台应用

在这个 5-10 分钟的 Visual Studio 集成开发环境 (IDE) 简介中，你将了解如何创建在控制台上运行的简单 Visual Basic 应用程序。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range=">=vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

## <a name="create-a-project"></a>创建项目

首先，先创建一个 Visual Basic 应用程序项目。 项目类型随附了所需的全部模板文件，无需添加任何内容！

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

1. 从顶部菜单栏中选择“文件”>“新建”>“项目”    。

1. 在“新建项目”对话框左侧的窗格中，展开“Visual Basic”，然后选择“.NET Core”。 在中间窗格中，选择“控制台应用(.NET Core)”。 随后将项目命名为 HelloWorld。

   ![Visual Studio IDE 中“新建项目”对话框中的控制台应用 (.NET Core) 项目模板](../ide/media/new-project-vb-dotnetcore-helloworld-console-app.png)

   如果没有看到“控制台应用(.NET Core)”项目模板，请单击“新建项目”对话框左侧窗格中的“打开 Visual Studio 安装程序”链接。

   ![单击“新建项目”对话框中的“打开 Visual Studio 安装程序”链接](../ide/media/vb-open-visual-studio-installer-hello-world.png)

   Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改” 。

   ![Visual Studio 安装程序中的 .NET Core 跨平台开发工作负荷](../ide/media/dot-net-core-xplat-dev-workload.png)

::: moniker-end

::: moniker range="vs-2019"

> [!NOTE]
> 本快速入门中的部分屏幕截图使用深色主题。 如果没有深色主题但想要使用，请参阅[个性化设置 Visual Studio IDE 和编辑器](quickstart-personalize-the-ide.md)页面，了解具体方法。

1. 打开 Visual Studio。

1. 在“开始”窗口上，选择“创建新项目”  。

   ![显示 Visual Studio 中的“开始”窗口的屏幕截图，其中突出显示了“创建新项目”选项。](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. 在“创建新项目”窗口中，从“语言”列表中选择“Visual Basic”。 接下来，从“平台”列表中选择“Windows”，然后从“项目类型”列表中选择“控制台”。

   应用语言、平台和项目类型筛选器之后，选择“控制台应用程序”模板，然后选择“下一步” 。

   :::image type="content" source="../get-started/visual-basic/media/vs-2019/vb-create-new-project-console-net-core.png" alt-text="显示“创建新项目”窗口的屏幕截图，其中在语言、平台和项目类型筛选器中分别选择了“Visual Basic”、“Windows”和“控制台”。突出显示了“控制台应用程序”项目模板。":::

   > [!NOTE]
   > 如果未看到“控制台应用程序”模板，则可以通过“创建新项目”窗口安装该模板 。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > ![显示“找不到所需内容”消息中突出显示的“安装更多工具和功能”链接的屏幕截图。](../get-started/media/vs-2019/not-finding-what-looking-for.png) 
   > 
   > 然后，在 Visual Studio 安装程序中，选择“.NET Core 跨平台开发”工作负载  。
   >
   > ![显示 Visual Studio 安装程序中“.NET Core 跨平台开发”工作负载的屏幕截图。](../get-started/media/dot-net-core-xplat-dev-workload.png)
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 系统可能会提示你保存所有内容；如果出现提示，请按照指示进行操作。 接下来，选择“继续”，以安装工作负载  。 然后，返回到“[创建项目](#create-a-project)”过程中的步骤 2。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“HelloWorld”    。 然后，选择“下一步”。

   :::image type="content" source="../get-started/visual-basic/media/vs-2019/vb-name-your-console-project-hello-world.png" alt-text="显示“配置新项目”窗口的屏幕截图，其中“项目名称”字段中输入了“HelloWorld”。":::

1. 在“附加信息”窗口中，应已为目标框架选择“.NET Core 3.1” 。 如果未选择，则请选择“.NET Core 3.1”。 然后，选择“创建”。

   :::image type="content" source="../get-started/visual-basic/media/vs-2019/vb-target-framework.png" alt-text="显示“其他信息”窗口的屏幕截图，其中在“框架”字段中选择了“.NET Core 3.1”。":::

   此时，Visual Studio 将打开新项目。

::: moniker-end

::: moniker range=">=vs-2022"

1. 打开 Visual Studio。

1. 在“开始”窗口上，选择“创建新项目”  。

   :::image type="content" source="media/vs-2022/create-new-project-dark-theme.png" alt-text="显示 Visual Studio 中的“开始”窗口的屏幕截图，其中突出显示了“创建新项目”选项。":::

1. 在“创建新项目”窗口中，从“语言”列表中选择“Visual Basic”。 接下来，从“平台”列表中选择“Windows”，然后从“项目类型”列表中选择“控制台”。

   应用语言、平台和项目类型筛选器之后，选择“控制台应用程序”模板，然后选择“下一步” 。

   :::image type="content" source="media/vs-2022/vb-create-new-project-console-net-core.png" alt-text="显示“创建新项目”窗口的屏幕截图，其中在语言、平台和项目类型筛选器中分别选择了“Visual Basic”、“Windows”和“控制台”。突出显示了“控制台应用程序”项目模板。":::

   > [!NOTE]
   > 如果未看到“控制台应用程序”模板，则可以通过“创建新项目”窗口安装该模板 。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > :::image type="content" source="media/vs-2022/not-finding-what-looking-for.png" alt-text="显示“找不到所需内容”消息中突出显示的“安装更多工具和功能”链接的屏幕截图。":::
   > 
   > 然后在 Visual Studio 安装程序中，选择“.NET 桌面开发”工作负载。
   >
   > :::image type="content" source="media/vs-2022/dot-net-core-xplat-dev-workload.png" alt-text="显示 Visual Studio 安装程序中的“.NET 桌面开发”工作负载的屏幕截图。":::
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 系统可能会提示你保存所有内容；如果出现提示，请按照指示进行操作。 接下来，选择“继续”，以安装工作负载  。 然后，返回到“[创建项目](#create-a-project)”过程中的步骤 2。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“HelloWorld”    。 然后，选择“下一步”。

   :::image type="content" source="media/vs-2022/vb-name-your-project-hello-world.png" alt-text="显示“配置新项目”窗口的屏幕截图，其中“项目名称”字段中输入了“HelloWorld”。":::

1. 在“其他信息”窗口中，应已选择“.NET 6.0”作为目标框架 。 如果未选择，请在“框架”下拉列表中选择“.NET 6.0” 。 然后，选择“创建”。

   :::image type="content" source="media/vs-2022/vb-target-framework.png" alt-text="显示“其他信息”窗口的屏幕截图，其中在“框架”字段中选择了“.NET 6.0”。":::

   此时，Visual Studio 将打开新项目。

::: moniker-end

## <a name="create-the-application"></a>创建应用程序

::: moniker range="vs-2019"

选择 Visual Basic 项目模板并为项目命名后，Visual Studio 会创建一个简单的“Hello World”应用程序。 它通过调用 <xref:System.Console.WriteLine%2A> 方法在控制台窗口中 显示文本字符串“Hello World!”。

![显示 Visual Basic 项目模板中默认“Hello World”代码的屏幕截图。](../ide/media/vb-console-helloworld-template.png)

如果在 IDE 中选择“HelloWorld”按钮，则可以在调试模式下运行程序。

![显示 Visual Studio 工具栏中突出显示的“Hello World”按钮的屏幕截图。](../ide/media/vb-console-hello-world-button.png)

当应用程序在 Microsoft Visual Studio 调试控制台中运行时，控制台窗口会一直保持打开状态，直到你按下某个键。 

但是，如果你在文件资源管理器中导航到“HelloWorld.exe”并运行该文件，则 `Main` 过程将在其单个语句执行后终止，并且控制台窗口很快就会关闭。

### <a name="add-some-code&quot;></a>添加一些代码

先添加一些代码来暂停应用程序，然后请求用户输入。

1. 在 <xref:System.Console.WriteLine%2A> 方法调用后面紧接着添加以下代码：

   ```vb
   Console.Write(&quot;Press any key to continue...")
   Console.ReadKey(true)
   ```

   此时程序暂停，直到按下某个键。

1. 在菜单栏上，选择“生成”>“生成解决方案” 。

   这会将程序编译成一种中间语言 (IL)，然后由实时 (JIT) 编译器转换成二进制代码。

## <a name="run-the-application"></a>运行应用程序

1. 在“解决方案资源管理器”中，右键单击“HelloWorld”打开项目的上下文菜单 。 然后选择“在文件资源管理器中打开文件夹”。

1. 导航到“bin > Debug > net6.0”文件夹中的“HelloWorld.exe”文件并运行该文件。

现在，该应用程序已在控制台中运行，并且在你按下任意键关闭控制台窗口之前，它会一直保持打开状态。

   ![显示正在运行的 Hello World 控制台应用程序的屏幕截图。 该应用显示了消息“Hello World!” 以及“Press any key to continue”。](../ide/media/vb-console-hello-world-press-any-key.png)

::: moniker-end

::: moniker range=">=vs-2022&quot;

选择 Visual Basic 项目模板并为项目命名后，Visual Studio 会创建一个简单的“Hello World!” 应用程序。 Program.vb 文件包含默认代码，该代码调用 <xref:System.Console.WriteLine%2A> 方法以在控制台窗口中 显示文本字符串“Hello World!”。

:::image type="content" source="media/vs-2022/vb-console-hello-world-template.png" alt-text="显示 Program.vb 文件中默认“Hello World”代码的屏幕截图。":::

选择“HelloWorld”按钮或按 Ctrl+F5，以在调试模式下运行默认“HelloWorld”代码  。

:::image type="content" source="media/vs-2022/vb-console-hello-world-button.png" alt-text="显示 Visual Studio 工具栏中突出显示的“HelloWorld”按钮的屏幕截图。":::

当应用程序在 Microsoft Visual Studio 调试控制台中运行时，控制台窗口会一直保持打开状态，直到你按下某个键。 

但是，如果你在文件资源管理器中导航到“HelloWorld.exe”并运行该文件，则 `Main` 过程将在其单个语句执行后终止，并且控制台窗口很快就会关闭。

### <a name=&quot;add-some-code&quot;></a>添加一些代码

先添加一些代码来暂停应用程序，然后请求用户输入。

1. 在 <xref:System.Console.WriteLine%2A> 方法调用后面紧接着添加以下代码：

   ```vb
   Console.Write(&quot;Press any key to continue...")
   Console.ReadKey(true)
   ```

   此代码会一直将程序暂停，直到你按下某个键。

1. 在菜单栏上，选择“生成”>“生成解决方案” 。

   生成解决方案，将程序编译成一种由实时 (JIT) 编译器转换成二进制代码的中间语言 (IL)。

## <a name="run-the-application"></a>运行应用程序

1. 在“解决方案资源管理器”中，右键单击“HelloWorld”打开项目的上下文菜单 。 然后选择“在文件资源管理器中打开文件夹”。

1. 导航到“bin > Debug > net6.0”文件夹中的“HelloWorld.exe”文件并运行该文件。

现在，该应用程序已在控制台中运行，并且在你按下任意键关闭控制台窗口之前，它会一直保持打开状态。

   :::image type="content" source="media/vs-2022/vb-console-hello-world-press-any-key.png" alt-text="显示正在运行的 HelloWorld 控制台应用程序的屏幕截图。应用显示了消息“Hello World!”和“Press any key to continue”":::。

::: moniker-end

## <a name="next-steps"></a>后续步骤

祝贺你完成此快速入门！ 希望你已对 Visual Basic 和 Visual Studio IDE 有了一定了解。 若要更加深入地了解，请继续学习下面的教程。

> [!div class="nextstepaction"]
> [Visual Studio 中的 Visual Basic 入门](../get-started/visual-basic/tutorial-console.md)
