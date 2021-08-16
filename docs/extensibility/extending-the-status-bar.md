---
title: 扩展状态栏|Microsoft Docs
description: 了解如何扩展 IDE 底部的Visual Studio状态栏，该状态栏显示信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- status bars, about status bars
- status bars, overview
ms.assetid: f955115c-4c5f-45ec-b41b-365868c5ec0c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: aa0acbd99328b55f0a15335572a0a185e1394ee85cc992cf71a59c2f52e1d9de
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414891"
---
# <a name="extend-the-status-bar"></a>扩展状态栏
可以使用 IDE Visual Studio的状态栏来显示信息。

 扩展状态栏时，可以在四个区域显示信息和 UI：反馈区域、进度栏、动画区域以及设计器区域。 使用反馈区域可以显示文本并突出显示显示的文本。 进度栏显示短时间运行操作（如保存文件）的增量进度。 动画区域为长时间运行的操作或不确定长度的操作（例如，在解决方案中生成多个项目）显示连续循环动画。 设计器区域显示光标位置的行号和列号。

 可以使用来自服务请求的接口 (<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar> 获取 <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> 状态) 。 此外，位于窗口框架上的任何对象都可以通过实现 接口注册为状态栏客户端 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> 对象。 每当激活窗口时，Visual Studio查询该窗口上所站点的对象以寻找 `IVsStatusbarUser` 接口。 如果找到，它会在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> 返回的接口上调用 方法，对象可以从该方法中更新状态栏。 例如，文档窗口可以使用 方法在设计器 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> 区域处于活动状态时更新它们的信息。

 以下过程假定你了解如何创建 VSIX 项目并添加自定义菜单命令。 有关信息，请参阅 [使用菜单命令 创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="modify-the-status-bar"></a>修改状态栏
 此过程演示如何设置和获取文本、显示静态文本，以及突出显示状态栏的反馈区域中显示的文本。

### <a name="read-and-write-to-the-status-bar"></a>读取和写入状态栏

1. 创建名为 **TestStatusBarExtension** 的 VSIX 项目，并添加名为 **TestStatusBarCommand** 的菜单命令。

2. 在 *TestStatusBarCommand.cs* 中，将命令处理程序方法代码 () `MenuItemCallback` 替换为以下内容：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        IVsStatusbar statusBar = (IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));

        // Make sure the status bar is not frozen
        int frozen;

        statusBar.IsFrozen(out frozen);

        if (frozen != 0)
        {
            statusBar.FreezeOutput(0);
        }

        // Set the status bar text and make its display static.
        statusBar.SetText("We just wrote to the status bar.");

        // Freeze the status bar.
        statusBar.FreezeOutput(1);

        // Get the status bar text.
        string text;
        statusBar.GetText(out text);
        System.Windows.Forms.MessageBox.Show(text);

        // Clear the status bar text.
        statusBar.FreezeOutput(0);
        statusBar.Clear();
    }
    ```

3. 编译代码并开始调试。

4. 打开 **Visual Studio** 实验实例中的"工具"Visual Studio。 单击" **调用 TestStatusBarCommand"** 按钮。

     应会看到状态栏中的文本现在显示为 **"我们刚刚写入状态栏"。** 和显示的消息框具有相同的文本。

### <a name="update-the-progress-bar"></a>更新进度栏

1. 此过程将展示如何初始化和更新进度栏。

2. 打开 *TestStatusBarCommand.cs* 文件，将 `MenuItemCallback` 方法替换为以下代码：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        IVsStatusbar statusBar = (IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));
        uint cookie = 0;
        string label = "Writing to the progress bar";

        // Initialize the progress bar.
        statusBar.Progress(ref cookie, 1, "", 0, 0);

        for (uint i = 0, total = 20; i <= total; i++)
        {
            // Display progress every second.
            statusBar.Progress(ref cookie, 1, label, i, total);
            System.Threading.Thread.Sleep(1000);
        }

        // Clear the progress bar.
        statusBar.Progress(ref cookie, 0, "", 0, 0);
    }
    ```

3. 编译代码并开始调试。

4. 打开 **Visual Studio** 实验实例中的"工具"Visual Studio。 单击 **"调用 TestStatusBarCommand"** 按钮。

     应会看到状态栏中的文本现在显示为" **写入进度栏"。** 还应看到进度栏每隔 20 秒更新一次。 之后，状态栏和进度栏将被清除。

### <a name="display-an-animation"></a>显示动画

1. 状态栏显示一个循环动画，该动画指示长时间运行的操作 (例如，在解决方案中生成多个) 。 如果未看到此动画，请确保具有正确的 **"工具选项**  >  **"** 设置：

     转到"**工具选项**  >    >  **""常规**"选项卡，取消选中 **"根据客户端性能自动调整视觉体验"。** 然后选中子选项"启用 **丰富的客户端视觉体验"。** 现在，当你在项目的实验实例中生成项目时，你应该能够看到Visual Studio。

     在此过程中，我们将显示Visual Studio生成项目或解决方案的标准动画。

2. 打开 *TestStatusBarCommand.cs* 文件，将 `MenuItemCallback` 方法替换为以下代码：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        IVsStatusbar statusBar =(IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));

        // Use the standard Visual Studio icon for building.
        object icon = (short)Microsoft.VisualStudio.Shell.Interop.Constants.SBAI_Build;

        // Display the icon in the Animation region.
        statusBar.Animation(1, ref icon);

        // The message box pauses execution for you to look at the animation.
        System.Windows.Forms.MessageBox.Show("showing?");

        // Stop the animation.
        statusBar.Animation(0, ref icon);
    }
    ```

3. 编译代码并开始调试。

4. 打开 **Visual Studio** 实验实例中的"工具"菜单，然后单击"**调用 TestStatusBarCommand"。**

     看到消息框时，还应在最右侧状态栏中看到动画。 关闭消息框时，动画将消失。
