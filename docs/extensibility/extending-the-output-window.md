---
title: 扩展输出窗口 |Microsoft Docs
description: 了解如何扩展 Visual Studio SDK 中的"输出"窗口，以及如何创建和管理自己的自定义窗格。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Output window, about Output window
ms.assetid: b02fa88c-f92a-4ff6-ba5f-2eb4d48a643a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b7b0ba71fa7f1c20d53a084580546d6e85bd0f03515b859589c664e11f0910dd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121305966"
---
# <a name="extend-the-output-window"></a>扩展"输出"窗口
" **输出** "窗口是一组读/写文本窗格。 Visual Studio具有以下内置窗格：生成 ，其中项目传达有关生成的消息;常规 ，其中传达有关 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE 的消息。 项目通过接口方法自动获取对"生成"窗格的引用，Visual Studio服务提供对"常规" <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> 窗格的 <xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane> 直接访问。 除了内置窗格，还可以创建和管理自己的自定义窗格。

 可以通过 和 **接口** 直接控制"输出 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> "窗口。 由服务提供的 接口定义用于创建、检索和销毁"输出 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> **"窗口** 窗格的方法。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane>接口定义用于显示窗格、隐藏窗格和操作其文本的方法。 控制"输出 **"窗口的另** 一种方式是通过自动化对象模型中的 <xref:EnvDTE.OutputWindow> Visual Studio <xref:EnvDTE.OutputWindowPane> 对象。 这些对象封装 和 接口的几乎所有 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> 功能。 此外， 和 对象还添加了一些更高级别的功能，以便更轻松地枚举"输出"窗口窗格以及从窗格中 <xref:EnvDTE.OutputWindow> <xref:EnvDTE.OutputWindowPane> 检索文本。 

## <a name="create-an-extension-that-uses-the-output-pane"></a>创建使用"输出"窗格的扩展
 你可以创建一个扩展，用于练习"输出"窗格的不同方面。

1. 使用名为 TestOutput 的菜单命令创建名为 的 VSIX `TestOutput` **项目**。 有关详细信息，请参阅 [使用菜单命令 创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 添加以下引用：

    1. EnvDTE

    2. EnvDTE80

3. 在 *TestOutput.cs* 中，添加以下 using 语句：

    ```f#
    using EnvDTE;
    using EnvDTE80;
    ```

4. 在 *TestOutput.cs 中*，删除 `ShowMessageBox` 方法。 添加以下方法存根：

    ```csharp
    private void OutputCommandHandler(object sender, EventArgs e)
    {
    }
    ```

5. 在 TestOutput 构造函数中，将命令处理程序更改为 OutputCommandHandler。 下面是添加命令的部分：

    ```csharp
    OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
    if (commandService != null)
    {
        CommandID menuCommandID = new CommandID(MenuGroup, CommandId);
        EventHandler eventHandler = OutputCommandHandler;
        MenuCommand menuItem = new MenuCommand(eventHandler, menuCommandID);
        commandService.AddCommand(menuItem);
    }
    ```

6. 以下各节具有不同的方法，用于显示处理"输出"窗格的不同方法。 可以将这些方法调用到 方法 `OutputCommandHandler()` 的正文中。 例如，以下代码将添加 `CreatePane()` 下一节中给定的 方法。

    ```csharp
    private void OutputCommandHandler(object sender, EventArgs e)
    {
        CreatePane(new Guid(), "Created Pane", true, false);
    }
    ```

## <a name="create-an-output-window-with-ivsoutputwindow"></a>使用 IVsOutputWindow 创建输出窗口
 此示例演示如何使用 接口创建新的 **"** 输出"窗口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> 窗格。

```csharp
void CreatePane(Guid paneGuid, string title,
    bool visible, bool clearWithSolution)
{
    IVsOutputWindow output =
        (IVsOutputWindow)GetService(typeof(SVsOutputWindow));
    IVsOutputWindowPane pane;

    // Create a new pane.
    output.CreatePane(
        ref paneGuid,
        title,
        Convert.ToInt32(visible),
        Convert.ToInt32(clearWithSolution));

    // Retrieve the new pane.
    output.GetPane(ref paneGuid, out pane);

     pane.OutputString("This is the Created Pane \n");
}
```

 如果将此方法添加到上一部分中给定的扩展，则单击 **"调用 TestOutput"** 命令时，应会看到"输出"窗口，其标题为"显示来自 **：CreatedPane** 的输出"和单词"这是窗格本身的已创建窗格"。

## <a name="create-an-output-window-with-outputwindow"></a>使用 OutputWindow 创建输出窗口
 此示例演示如何使用 **对象创建** "输出"窗口 <xref:EnvDTE.OutputWindow> 窗格。

```csharp
void CreatePane(string title)
{
    DTE2 dte = (DTE2)GetService(typeof(DTE));
    OutputWindowPanes panes =
        dte.ToolWindows.OutputWindow.OutputWindowPanes;

    try
    {
        // If the pane exists already, write to it.
        panes.Item(title);
    }
    catch (ArgumentException)
    {
        // Create a new pane and write to it.
        panes.Add(title);
    }
}
```

 尽管集合允许按标题检索"输出"窗口窗格，但不能保证窗格标题 <xref:EnvDTE.OutputWindowPanes> 是唯一的。  如果怀疑标题的唯一性，请使用 方法按 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow.GetPane%2A> GUID 检索正确的窗格。

 如果将此方法添加到上一节中给定的扩展，则单击 **"调用 TestOutput"** 命令时，应会看到"输出"窗口，其标头显示"显示输出来源 **：DTEPane"，** 窗格本身包含"已添加 **DTE** 窗格"字样。

## <a name="delete-an-output-window"></a>删除"输出"窗口
 此示例演示如何删除"输出 **"窗口** 窗格。

```csharp
void DeletePane(Guid paneGuid)
{
    IVsOutputWindow output =
    (IVsOutputWindow)ServiceProvider.GetService(typeof(SVsOutputWindow));

    IVsOutputWindowPane pane;
    output.GetPane(ref paneGuid, out pane);

    if (pane == null)
    {
        CreatePane(paneGuid, "New Pane\n", true, true);
    }
     else
    {
        output.DeletePane(ref paneGuid);
    }
}
```

 如果将此方法添加到上一节中给定的扩展，则单击 **"调用 TestOutput"** 命令时，应会看到"输出"窗口，其标题为"显示来自： **新建** 窗格的输出"，以及窗格本身中的"已添加 **的已创建** 窗格"字样。 如果再次单击 **"调用 TestOutput"** 命令，将删除该窗格。

## <a name="get-the-general-pane-of-the-output-window"></a>获取"输出"窗口的"常规"窗格
 此示例演示如何获取"输出" **窗口的内置** " **常规"** 窗格。

```csharp
IVsOutputWindowPane GetGeneralPane()
{
    return (IVsOutputWindowPane)GetService(
        typeof(SVsGeneralOutputWindowPane));
}
```

 如果将此方法添加到上一节中给定的扩展，则单击 **"调用 TestOutput"** 命令时，应会看到"输出"窗口在窗格中显示"**找到** 常规"窗格字样。

## <a name="get-the-build-pane-of-the-output-window"></a>获取"输出"窗口的"生成"窗格
 此示例演示如何查找"生成 **"窗格** 并写入。 由于 **"生成** "窗格默认未激活，因此也会激活它。

```csharp
void OutputTaskItemStringExExample(string buildMessage)
{
    EnvDTE80.DTE2 dte = (EnvDTE80.DTE2)ServiceProvider.GetService(typeof(EnvDTE.DTE));

    EnvDTE.OutputWindowPanes panes =
        dte.ToolWindows.OutputWindow.OutputWindowPanes;
    foreach (EnvDTE.OutputWindowPane pane in panes)
        {
            if (pane.Name.Contains("Build"))
            {
                pane.OutputString(buildMessage + "\n");
                pane.Activate();
                return;
             }
        }
}
```
