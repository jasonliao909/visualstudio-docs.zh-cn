---
title: 教程：创建简单的Visual Basic (VB) 控制台应用
description: 本教程介绍如何在 Visual Studio 中Visual Basic控制台应用程序。
ms.custom: vs-acquisition, get-started
ms.date: 02/09/2022
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: vb
author: anandmeg
ms.author: meghaanand
manager: jmartens
dev_langs:
- vb
ms.workload:
- multiple
ms.openlocfilehash: 2f138c1419fae42ca540abef832b35a375373818
ms.sourcegitcommit: a439b1878939b2364cee0d09b851c2a67c42e563
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2022
ms.locfileid: "138566554"
---
# <a name="tutorial-create-a-simple-visual-basic-vb-console-app"></a>教程：创建简单的Visual Basic (VB) 控制台应用

::: moniker range="vs-2017"

本文演示如何使用 Visual Studio创建简单的Visual Basic应用程序，即 *控制台应用*。 在此应用中，你要求用户输入其名称，然后用当前时间显示它。 你还将探索 [IDE Visual Studio 集成开发 (的](visual-studio-ide.md)) 。 Visual Basic 是一种易于学习的类型安全编程语言。 控制台应用获取输入，在命令行窗口（也称为控制台）中显示输出。

在本教程中，你将了解如何执行以下操作：

> [!div class="checklist"]
> - 创建 Visual Studio 项目
> - 运行默认应用程序
> - 添加用于请求用户输入的代码
> - 额外额度：添加两个数字
> - 清理资源

::: moniker-end

::: moniker range=">=vs-2019"

本文演示如何使用 Visual Studio创建简单的Visual Basic应用程序，即 *控制台应用*。 在此应用中，你要求用户输入其名称，然后用当前时间显示它。 你还将探索 IDE Visual Studio集成开发 (的) [功能](visual-studio-ide.md)，包括 [Git 中的源代码管理](/visualstudio/version-control)。 Visual Basic 是一种易于学习的类型安全编程语言。 控制台应用获取输入，在命令行窗口（也称为控制台）中显示输出。

在本教程中，你将了解如何执行以下操作：

> [!div class="checklist"]
> - 创建 Visual Studio 项目
> - 运行默认应用程序
> - 添加用于请求用户输入的代码
> - 额外额度：添加两个数字
> - 添加 Git 源代码管理
> - 清理资源

::: moniker-end

## <a name="prerequisites"></a>先决条件

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range=">=vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

## <a name="create-a-project"></a>创建项目

首先，你将创建一个Visual Basic应用项目。 默认项目模板包括可运行应用所需的所有文件。  

::: moniker range="<=vs-2019"

> [!NOTE]
> 本教程中的部分屏幕截图使用深色主题。 如果没有深色主题但想要使用，请参阅[个性化设置 Visual Studio IDE 和编辑器](../../ide/quickstart-personalize-the-ide.md)页面，了解具体方法。

::: moniker-end

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

2. 从顶部菜单栏中选择“文件”>“新建”>“项目”    。

3. 在“新建项目”对话框左侧的窗格中，展开“Visual Basic”，然后选择“.NET Core”。 在中间窗格中，选择“控制台应用(.NET Core)”。 随后将项目命名为“WhatIsYourName”。

   :::image type="content" source="media/new-project-vb-dotnetcore-whatisyourname-console-app.png" alt-text="Visual Studio IDE 中“新建项目”对话框中的控制台应用 (.NET Core) 项目模板":::

### <a name="add-a-workload-optional"></a>添加工作负载（可选）

如果未显示“控制台应用(.NET Core)”项目模板，可通过添加“.NET Core 跨平台开发”工作负载获取它。 可通过以下两种方式添加此工作负载，具体取决于计算机上安装的 Visual Studio 2017 更新。

#### <a name="option-1-use-the-new-project-dialog-box"></a>选项 1：使用“新建项目”对话框

1. 选择“新建项目”  对话框左窗格中的“打开 Visual Studio 安装程序”  链接。

   :::image type="content" source="../media/vs-open-visual-studio-installer-generic.png" alt-text="选择“新建项目”对话框中的“打开 Visual Studio 安装程序”链接":::

1. Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改” 。

   > :::image type="content" source="media/dot-net-core-xplat-dev-workload.png" alt-text="显示 Visual Studio 安装程序中“.NET Core 跨平台开发”工作负载的屏幕截图。":::

#### <a name="option-2-use-the-tools-menu-bar"></a>选项 2：使用“工具”菜单栏

1. 取消“新建项目”对话框，再从顶部菜单栏中选择“工具”>“获取工具和功能”  。

1. Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改” 。

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio 2019。

1. 在“开始”窗口上，选择“创建新项目”。

   :::image type="content" source="media/vs-2019/create-new-project-dark-theme.png" alt-text="显示 Visual Studio“开始”窗口的屏幕截图，其中选择了“创建新项目”。":::

1. 在“创建新项目”窗口中，从“语言”列表中选择“Visual Basic”。 接下来，从“平台”列表中选择“Windows”，然后从“项目类型”列表中选择“控制台”。

   应用这些语言、平台和项目类型筛选器后，选择"控制台 **应用程序** "模板，然后选择"下一步 **"**。

   :::image type="content" source="media/vs-2019/vb-create-new-project-console-net-core.png" alt-text="显示“创建新项目”窗口的屏幕截图，其中在“语言”、“平台”和“项目类型”筛选器中分别选择了“Visual Basic”、“Windows”和“控制台”，并且“控制台应用程序”项目模板处于选中状态。":::

   > [!NOTE]
   > 如果未看到“控制台应用程序”模板，则可以通过“创建新项目”窗口安装该模板 。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > :::image type="content" source="media/vs-2019/not-finding-what-looking-for.png" alt-text="显示“创建新项目”窗口内“找不到所需内容”消息中的“安装更多工具和功能”链接的屏幕截图。":::
   >
   > 然后，在 Visual Studio 安装程序中，选择“.NET Core 跨平台开发”工作负载  。
   >
   > :::image type="content" source="media/vs-2019/dot-net-core-xplat-dev-workload.png" alt-text="显示 Visual Studio 安装程序中“.NET Core 跨平台开发”工作负载的屏幕截图。":::
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 系统可能会提示你保存工作内容。 接下来，选择“继续”，以安装工作负载  。 然后，返回到此创建项目 [过程中的步骤 2](#create-a-project) 。

1. 在"**配置新项目"窗口中**，在"新建项目名称"框中Project *WhatIsYourName*" 。 然后，选择“下一步”。

   :::image type="content" source="media/vs-2019/vb-name-your-project-whatname.png" alt-text="显示“配置新项目”窗口的屏幕截图，其中“项目名称”字段已设置为“WhatIsYourName”。":::

1. 在" **其他信息"** 窗口中，应该已为目标框架 (. **NET 5.0**) 当前版本。 如果没有，请选择 **".NET 5.0 (当前)**"。 然后，选择“创建”  。

   :::image type="content" source="media/vs-2019/vb-target-framework.png" alt-text="显示&quot;其他信息&quot;窗口的屏幕截图，其中在&quot;目标框架&quot;字段中选择了&quot;.NET 5.0 (当前) &quot;。":::

   此时，Visual Studio 将打开新项目。

::: moniker-end

::: moniker range=">=vs-2022"

1. 打开 Visual Studio。

1. 在“开始”窗口上，选择“创建新项目”  。

   :::image type="content" source="media/vs-2022/create-new-project-dark-theme.png" alt-text="显示 Visual Studio“开始”窗口的屏幕截图，其中选择了“创建新项目”。":::

1. 在“创建新项目”窗口中，从“语言”列表中选择“Visual Basic”。 接下来，从“平台”列表中选择“Windows”，并从“项目类型”列表中选择“控制台” 。

   应用这些语言、平台和项目类型筛选器后，选择" **控制台应用** "模板，然后选择"下一步 **"**。

   :::image type="content" source="media/vs-2022/vb-create-new-project-console-net-core.png" alt-text="显示&quot;创建新项目&quot;窗口的屏幕截图，其中在&quot;语言、平台和 Project 类型筛选器&quot;中选择了&quot;Visual Basic&quot;、&quot;Windows&quot;和&quot;控制台&quot;，并且选择了&quot;控制台应用&quot;项目模板。":::

   > [!NOTE]
   > 如果未看到“控制台应用”模板，则可以通过“创建新项目”窗口安装该模板   。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > :::image type="content" source="media/vs-2022/not-finding-what-looking-for.png" alt-text="显示“创建新项目”窗口内“找不到所需内容”消息中的“安装更多工具和功能”链接的屏幕截图。":::
   >
   > 然后在 Visual Studio 安装程序中，选择“.NET 桌面开发”工作负载。
   >
   > :::image type="content" source="media/vs-2022/dot-net-core-xplat-dev-workload.png" alt-text="显示 Visual Studio 安装程序中的“.NET 桌面开发”工作负载的屏幕截图。":::
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 系统可能会提示你保存工作内容。 接下来，选择“继续”，以安装工作负载  。 然后，返回到此创建项目 [过程中的步骤 2](#create-a-project) 。

1. 在"**配置新项目"窗口中**，在"新建项目名称"框中Project *WhatIsYourName*" 。 然后，选择“下一步”。

   :::image type="content" source="media/vs-2022/vb-name-your-project-whatname.png" alt-text="显示“配置新项目”窗口的屏幕截图，其中“项目名称”字段已设置为“WhatIsYourName”。":::

1. 在“其他信息”窗口中，应已选择“.NET 6.0 (长期支持)”作为目标框架 。 如果没有，请选择“.NET 6.0 (长期支持)”。 然后，选择“创建”  。

   :::image type="content" source="media/vs-2022/vb-target-framework.png" alt-text="显示&quot;其他信息&quot;窗口的屏幕截图，其中在&quot;框架&quot;字段中 (选择了&quot;.NET 6.0) 长期支持&quot;。":::

   此时，Visual Studio 将打开新项目。

::: moniker-end

## <a name="run-the-app"></a>运行应用

选择 Visual Basic 项目模板并为项目命名后，Visual Studio 创建一个 *程序 .vb* 文件。 默认代码调用 <xref:System.Console.WriteLine%2A> 方法以显示文本字符串 "Hello World！" 显示文本字符串“Hello World!”。

可以通过两种方法在 *调试模式* 下 Visual Studio 中运行此代码，并从计算机将其作为常规 *独立* 应用运行。

### <a name="run-the-app-in-debug-mode"></a>在调试模式下运行应用

::: moniker range="vs-2017"

   :::image type="content" source="media/overview-ide-console-app.png" alt-text="显示 Visual Basic 项目模板中的默认 &quot;Hello World！&quot; 代码的屏幕截图。":::

1. 在调试模式下，选择 " **WhatIsYourName** " 按钮或按 **F5** 生成并运行默认的 "WhatIsYourName" 代码。

    :::image type="content" source="media/vb-ide-whatisyourname-button.png" alt-text="显示 Visual Studio 工具栏中突出显示 &quot;你的姓名&quot; 按钮的屏幕截图。":::

1. 当应用在 Microsoft Visual Studio 调试控制台中运行时，"Hello World！" 显示. 按任意键关闭调试控制台窗口并结束应用程序：

    :::image type="content" source="media/vb-console-hello-world-debug-dark.png" alt-text="显示 &quot;Hello World！&quot; 和 &quot;按任意键以关闭此窗口&quot; 消息的屏幕截图。":::

::: moniker-end

::: moniker range="vs-2019"

   :::image type="content" source="media/vs-2019/vb-ide-default-code.png" alt-text="显示默认 &quot;Hello World！&quot; 代码的屏幕截图。":::

1. 选择 **WhatIsYourName** 按钮，或按 **F5** 以调试模式运行默认代码。

   :::image type="content" source="media/vs-2019/vb-ide-whatisyourname-button.png" alt-text="显示 Visual Studio 工具栏中突出显示 &quot;你的姓名&quot; 按钮的屏幕截图。":::

1. 当应用在 Microsoft Visual Studio 调试控制台中运行时，"Hello World！" 显示. 按任意键关闭调试控制台窗口并结束应用程序：

    :::image type="content" source="media/vs-2019/vb-console-hello-world-press-any-key.png" alt-text="显示 &quot;Hello World！&quot; 和 &quot;按任意键以关闭此窗口&quot; 消息的屏幕截图。":::

::: moniker-end

::: moniker range=">=vs-2022"

   :::image type="content" source="media/vs-2022/vb-ide-default-code.png" alt-text="显示默认 &quot;Hello World！&quot; 代码的屏幕截图。":::

1. 选择 **WhatIsYourName** 按钮，或按 **F5** 以调试模式运行默认代码。

   :::image type="content" source="media/vs-2022/vb-ide-whatisyourname-button.png" alt-text="显示 Visual Studio 工具栏中突出显示 &quot;你的姓名&quot; 按钮的屏幕截图。":::

1. 当应用在 Microsoft Visual Studio 调试控制台中运行时，"Hello World！" 显示. 按任意键关闭调试控制台窗口并结束应用程序：

    :::image type="content" source="media/vs-2022/vb-console-hello-world-press-any-key.png" alt-text="显示 &quot;Hello World！&quot; 和 &quot;按任意键以关闭此窗口&quot; 消息的屏幕截图。":::

::: moniker-end

### <a name="run-the-app-as-a-standalone"></a>以独立方式运行应用

若要查看 Visual Studio 之外的输出，请在系统控制台窗口中生成并运行可执行文件 (.exe 文件) 。 

::: moniker range="vs-2017"

1. 在 " **生成** " 菜单中，选择 " **生成解决方案**"。

1. 在 **解决方案资源管理器** 中，右键单击 **WhatIsYourName** ，然后选择 " **在文件资源管理器中打开文件**"。

1. 在 **文件资源管理器** 中，导航到 **bin\Debug\netcoreapp 3.1** 目录并运行 **WhatIsYourName.exe**。

1. 该 `Main` 过程在其单个语句执行后终止，控制台窗口会立即关闭。 若要使控制台在用户按下某个键之前可见，请参阅下一节。

::: moniker-end

::: moniker range="vs-2019"

1. 在 " **生成** " 菜单中，选择 " **生成解决方案**"。

1. 在 **解决方案资源管理器** 中，右键单击 **WhatIsYourName** ，然后选择 " **在文件资源管理器中打开文件**"。

1. 在 **文件资源管理器** 中，导航到 **bin\Debug\net 5.0** 目录并运行 **WhatIsYourName.exe**。

1. 该 `Main` 过程在其单个语句执行后终止，控制台窗口会立即关闭。 若要使控制台在用户按下某个键之前可见，请参阅下一节。

::: moniker-end

::: moniker range="vs-2022"

1. 在 " **生成** " 菜单中，选择 " **生成解决方案**"。

1. 在 **解决方案资源管理器** 中，右键单击 **WhatIsYourName** ，然后选择 " **在文件资源管理器中打开文件**"。

1. 在 **文件资源管理器** 中，导航到 **bin\Debug\core6.0** 目录并运行 **WhatIsYourName.exe**。

1. 该 `Main` 过程在其单个语句执行后终止，控制台窗口会立即关闭。 若要使控制台在用户按下某个键之前可见，请参阅下一节。

::: moniker-end

## <a name="add-code-to-ask-for-user-input"></a>添加代码以请求用户输入

接下来，你将添加提示你输入名称的 Visual Basic 代码，然后将其与当前日期和时间一起显示。 此外，你将添加用于暂停控制台窗口的代码，直到用户按下某个键。

::: moniker range="vs-2017"

1. 在行之后 `Sub Main(args As String())` 和行前 `End Sub` 输入以下 Visual Basic 代码，并替换 <xref:System.Console.WriteLine%2A> 行：

     ```vb
     Console.Write("Please enter your name: ")
     Dim name = Console.ReadLine()
     Dim currentDate = DateTime.Now
     Console.WriteLine($"Hello, {name}, on {currentDate:d} at {currentDate:t}")
     Console.Write("Press any key to continue...")
     Console.ReadKey(True)
     ```

   - <xref:System.Console.Write%2A> 并 <xref:System.Console.WriteLine%2A> 将字符串写入控制台。 
   - <xref:System.Console.ReadLine%2A> 从控制台读取输入，在本例中为字符串。 
   - <xref:System.DateTime> 表示日期时间，并 <xref:System.DateTime.Now> 返回当前时间。 
   - <xref:System.Console.ReadKey> 暂停应用并等待按键。

   :::image type="content" source="media/vb-code-window-whatisyourname-dark.png" alt-text="显示 Visual Basic 代码编辑器中加载的 &quot;WhatIsYourName&quot; 项目中 &quot;Program&quot; 文件的代码的屏幕截图。":::

1. 选择 **WhatIsYourName** 按钮或按 **F5** 以在调试模式下生成并运行第一个应用。

1. 当 "调试控制台" 窗口打开时，请输入您的名称。 控制台窗口应如以下屏幕快照所示：

   :::image type="content" source="media/vs-2019/vb-console-enter-your-name.png" alt-text="显示 &quot;调试控制台&quot; 窗口的屏幕截图，其中包含 &quot;请输入您的姓名&quot;、日期和时间，以及 &quot;按任意键继续&quot; 消息。":::

1. 按任意键结束应用程序，然后按任意键关闭 "调试控制台" 窗口。

::: moniker-end

::: moniker range="vs-2019"

1. 在行之后 `Sub Main(args As String())` 和行前 `End Sub` 输入以下 Visual Basic 代码，并替换 <xref:System.Console.WriteLine%2A> 行：

     ```vb
     Console.Write("Please enter your name: ")
     Dim name = Console.ReadLine()
     Dim currentDate = DateTime.Now
     Console.WriteLine($"Hello, {name}, on {currentDate:d} at {currentDate:t}")
     Console.Write("Press any key to continue...")
     Console.ReadKey(True)
     ```

   - <xref:System.Console.Write%2A> 并 <xref:System.Console.WriteLine%2A> 将字符串写入控制台。 
   - <xref:System.Console.ReadLine%2A> 从控制台读取输入，在本例中为字符串。 
   - <xref:System.DateTime> 表示日期时间，并 <xref:System.DateTime.Now> 返回当前时间。 
   - <xref:System.Console.ReadKey> 暂停应用并等待按键。

   :::image type="content" source="media/vs-2019/vb-code-window-whatisyourname-dark.png" alt-text="显示 Visual Basic 代码编辑器中加载的 &quot;WhatIsYourName&quot; 项目中 &quot;Program&quot; 文件的代码的屏幕截图。":::

1. 选择 **WhatIsYourName** 按钮或按 **F5** 以在调试模式下生成并运行第一个应用。

1. 当 "调试控制台" 窗口打开时，请输入您的名称。 控制台窗口应如以下屏幕快照所示：

   :::image type="content" source="media/vs-2019/vb-console-enter-your-name.png" alt-text="显示 &quot;调试控制台&quot; 窗口的屏幕截图，其中包含 &quot;请输入您的姓名&quot;、日期和时间，以及 &quot;按任意键继续&quot; 消息。":::

1. 按任意键结束应用程序，然后按任意键关闭 "调试控制台" 窗口。

::: moniker-end

::: moniker range=">=vs-2022"

1. 在行之后 `Sub Main(args As String())` 和行前 `End Sub` 输入以下 Visual Basic 代码，并替换 <xref:System.Console.WriteLine%2A> 行：

     ```vb
     Console.Write("Please enter your name: ")
     Dim name = Console.ReadLine()
     Dim currentDate = DateTime.Now
     Console.WriteLine($"Hello, {name}, on {currentDate:d} at {currentDate:t}")
     Console.Write("Press any key to continue...")
     Console.ReadKey(True)
     ```

   - <xref:System.Console.Write%2A> 并 <xref:System.Console.WriteLine%2A> 将字符串写入控制台。 
   - <xref:System.Console.ReadLine%2A> 从控制台读取输入，在本例中为字符串。 
   - <xref:System.DateTime> 表示日期时间，并 <xref:System.DateTime.Now> 返回当前时间。 
   - <xref:System.Console.ReadKey> 暂停应用并等待按键。

   :::image type="content" source="media/vs-2022/vb-code-window-whatisyourname-dark.png" alt-text="显示 Visual Basic 代码编辑器中加载的 &quot;WhatIsYourName&quot; 项目中 &quot;Program&quot; 文件的代码的屏幕截图。":::

1. 选择 **WhatIsYourName** 按钮或按 **F5** 以在调试模式下生成并运行第一个应用。

1. 当 "调试控制台" 窗口打开时，请输入您的名称。 控制台窗口应如以下屏幕快照所示：

   :::image type="content" source="media/vs-2022/vb-console-enter-your-name.png" alt-text="显示 &quot;调试控制台&quot; 窗口的屏幕截图，其中包含 &quot;请输入您的姓名&quot;、日期和时间，以及 &quot;按任意键继续&quot; 消息。":::

1. 按任意键结束应用程序，然后按任意键关闭 "调试控制台" 窗口。

::: moniker-end

现在，你的新代码已在应用程序中，生成并运行系统控制台窗口中的可执行文件 (.exe 文件) ，如前文所述，将 [该应用程序作为独立运行](#run-the-app-as-a-standalone)。 现在，按下某个键时，应用程序退出，这会关闭控制台窗口。

## <a name="extra-credit-add-two-numbers"></a>额外信用额度：添加两个数字

此示例演示如何读取数字而不是字符串，并进行一些算术运算。 尝试更改你的代码：

```vb
Module Program
    Sub Main(args As String())
        Console.Write("Please enter your name: ")
        Dim name = Console.ReadLine()
        Dim currentDate = DateTime.Now
        Console.WriteLine($"Hello, {name}, on {currentDate:d} at {currentDate:t}")
        Console.Write("Press any key to continue...")
        Console.ReadKey(True)
    End Sub
End Module
```

更改为：

```vb
Module Program
    Public num1 As Integer
    Public num2 As Integer
    Public answer As Integer
    Sub Main(args As String())
        Console.Write("Type a number and press Enter")
        num1 = Console.ReadLine()
        Console.Write("Type another number to add to it and press Enter")
        num2 = Console.ReadLine()
        answer = num1 + num2
        Console.WriteLine("The answer is " & answer)
        Console.Write("Press any key to continue...")
        Console.ReadKey(True)
    End Sub
End Module
```

然后运行更新的应用程序，如 "[运行应用程序](#run-the-app)" 中所述。

[!INCLUDE[../includes/git-source-control.md](../includes/git-source-control.md)]

## <a name="clean-up-resources"></a>清理资源

如果不打算继续使用此应用，请删除该项目。

1. 在 **解决方案资源管理器** 中，右键单击 " **WhatIsYourName** " 打开项目的上下文菜单。 然后选择“在文件资源管理器中打开文件夹”。

1. 关闭 Visual Studio。

1. 在 " **文件资源管理器** " 对话框中，打开两个级别的文件夹。

1. 右键单击 **WhatIsYourName** 文件夹，然后选择 " **删除**"。

## <a name="next-steps"></a>后续步骤

恭喜你完成本教程！ 若要了解详细信息，请参阅以下教程。

> [!div class="nextstepaction"]
> [在 Visual Studio 中使用 Visual Basic 和 .NET Core SDK 生成库](/dotnet/core/tutorials/vb-library-with-visual-studio)

## <a name="see-also"></a>另请参阅

* [Visual Basic 语言演练](/dotnet/visual-basic/walkthroughs)
* [Visual Basic 语言参考](/dotnet/visual-basic/language-reference/index)
* [Visual Basic 代码文件的 IntelliSense](../../ide/visual-basic-specific-intellisense.md)
