---
title: 使用菜单命令创建扩展|Microsoft Docs
description: 了解如何使用菜单命令创建扩展，以启动记事本。 创建菜单命令，然后更改菜单命令处理程序。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- write a vspackage
- vspackage
- tutorials
- visual studio package
ms.assetid: f97104c8-2bcb-45c7-a3c9-85abeda8df98
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: d6fe7776e331fc9918035cb9c9edc7e8cf4c8ae9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600983"
---
# <a name="create-an-extension-with-a-menu-command"></a>使用菜单命令创建扩展

本演练演示如何使用菜单命令创建扩展，以启动记事本。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-a-menu-command"></a>创建菜单命令

1. 创建名为 **FirstMenuCommand** 的 VSIX 项目。 可以通过搜索"vsix"在"新建Project"找到 VSIX 项目模板。 

::: moniker range="vs-2017"

2. 项目打开时，添加名为 **FirstCommand 的自定义命令项模板**。 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 在"**添加新项"对话框中**，转到 **"Visual C#**  >  **扩展性"，** 然后选择"**自定义命令"。** 在 **窗口底部的** "名称"字段中，将命令文件名更改为 *FirstCommand.cs*。

::: moniker-end

::: moniker range=">=vs-2019"

2. 项目打开时，添加名为 **FirstCommand 的自定义命令项模板**。 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 在"**添加新项"对话框中**，转到 **"Visual C#**  >  **扩展性"，** 然后选择"命令 **"。** 在 **窗口底部的** "名称"字段中，将命令文件名更改为 *FirstCommand.cs*。

::: moniker-end

3. 生成项目并启动调试。

    将显示该实例的Visual Studio实例。 有关实验实例的信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。

::: moniker range="vs-2017"

4. 在实验实例中，打开"**工具**  >  **扩展和更新"** 窗口。 应在此处看到 **FirstMenuCommand** 扩展。  (如果在应用程序 **的工作** 实例中打开"扩展和更新Visual Studio，则看不到 **FirstMenuCommand**) 。

::: moniker-end

::: moniker range=">=vs-2019"

4. 在实验实例中，打开 **"扩展**  >  **管理扩展"** 窗口。 应在此处看到 **FirstMenuCommand** 扩展。  (如果在 Visual Studio 的工作实例中打开"管理扩展"，则看不到 **FirstMenuCommand**) 。

::: moniker-end

现在转到实验 **实例中的** "工具"菜单。 应会看到 **Invoke FirstCommand** 命令。 此时，该命令将打开一个消息框，显示 **FirstCommand Inside FirstMenuCommand.FirstCommand.MenuItemCallback** () 。 下一部分将了解如何记事本此命令开始运行。

## <a name="change-the-menu-command-handler"></a>更改菜单命令处理程序

现在，让我们更新命令处理程序以启动记事本。

1. 停止调试并返回到工作实例Visual Studio。 打开 *FirstCommand.cs 文件* 并添加以下 using 语句：

    ```csharp
    using System.Diagnostics;
    ```

2. 查找专用 FirstCommand 构造函数。 这是将命令挂钩到命令服务并指定命令处理程序的位置。 将命令处理程序的名称更改为 StartNotepad，如下所示：

    ```csharp
    private FirstCommand(AsyncPackage package, OleMenuCommandService commandService)
    {
        this.package = package ?? throw new ArgumentNullException(nameof(package));
        commandService = commandService ?? throw new ArgumentNullException(nameof(commandService));

        CommandID menuCommandID = new CommandID(CommandSet, CommandId);
        // Change to StartNotepad handler.
        MenuCommand menuItem = new MenuCommand(this.StartNotepad, menuCommandID);
        commandService.AddCommand(menuItem);
    }
    ```

3. 删除 `Execute` 方法并添加 `StartNotepad` 方法，该方法将启动记事本：

    ```csharp
    private void StartNotepad(object sender, EventArgs e)
    {
        ThreadHelper.ThrowIfNotOnUIThread();

        Process proc = new Process();
        proc.StartInfo.FileName = "notepad.exe";
        proc.Start();
    }
    ```

4. 现在尝试一下。开始调试项目并单击"工具  >  **""调用 FirstCommand"** 时，应会看到记事本实例。

    可以使用 类的实例来运行 <xref:System.Diagnostics.Process> 任何可执行文件，而不只是记事本。 例如，使用 `calc.exe` 试用。

## <a name="clean-up-the-experimental-environment"></a>清理实验性环境

如果要开发多个扩展，或只是使用不同版本的扩展代码探索结果，则实验性环境可能会停止以预期方式工作。 在这种情况下，应运行重置脚本。 它称为"**重置** Visual Studio实例"，它作为 Visual Studio SDK 的一部分提供。 此脚本从实验性环境中删除对扩展的所有引用，以便你可以从头开始。

可以通过两种方式之一访问此脚本：

1. 在桌面上，找到 **"重置Visual Studio实例"。**

2. 从命令行运行以下命令：

    ```cmd
    <VSSDK installation>\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe /Reset /VSInstance=<version> /RootSuffix=Exp && PAUSE

    ```

## <a name="deploy-your-extension"></a>部署扩展

现在，你的工具扩展已以你想要的方式运行，现在可以考虑与朋友和同事共享它了。 只要安装了 2015 Visual Studio，这很容易。 你可做的就是将你构建的 *.vsix* 文件发送给他们。  (请务必在发布模式.) 

可以在 *FirstMenuCommand* bin 目录中找到此扩展的 *.vsix* 文件。 具体而言，假设你已生成发布配置，它将在：

*\<code directory>\FirstMenuCommand\FirstMenuCommand\bin\Release\FirstMenuCommand.vsix*

若要安装扩展，你的好友需要关闭 Visual Studio 的所有打开实例，然后双击 *.vsix* 文件，这将打开 **VSIX 安装程序**。 文件将复制到 *%LocalAppData%\Microsoft\VisualStudio \<version> \Extensions* 目录。

当你的好友再次Visual Studio，他们将在"工具扩展和更新"中查找 FirstMenuCommand  >  **扩展**。 他们也可以转到 **"扩展和更新"** 来卸载或禁用扩展。

## <a name="next-steps"></a>后续步骤

本演练只演示了使用扩展插件可以执行Visual Studio部分。 下面是其他扩展的简短 (，) 扩展可以执行Visual Studio操作：

1. 可以使用简单的菜单命令执行更多操作：

   1. 添加自己的图标： [向菜单命令添加图标](../extensibility/adding-icons-to-menu-commands.md)

   2. 更改菜单命令的文本 [：更改菜单命令的文本](../extensibility/changing-the-text-of-a-menu-command.md)

   3. 向命令添加菜单快捷方式 [：将键盘快捷方式绑定到菜单项](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)

2. 添加不同类型的命令、菜单和工具栏： [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)

3. 添加工具窗口并扩展内置工具Visual Studio：[扩展和自定义工具窗口](../extensibility/extending-and-customizing-tool-windows.md)

4. 将 IntelliSense、代码建议和其他功能添加到现有代码编辑器： [扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)

5. 将"选项"和"属性"页和用户设置添加到扩展： [扩展属性和"属性"窗口](../extensibility/extending-properties-and-the-property-window.md) 和 ["扩展用户设置和选项"](../extensibility/extending-user-settings-and-options.md)

   其他类型的扩展需要更多的工作，例如创建一种新类型的项目 ([扩展](../extensibility/extending-projects.md)项目) 、创建新的编辑器类型 ([创建自定义](../extensibility/creating-custom-editors-and-designers.md)编辑器和设计器) 或在独立的 shell 中实现扩展[：Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)独立 shell
