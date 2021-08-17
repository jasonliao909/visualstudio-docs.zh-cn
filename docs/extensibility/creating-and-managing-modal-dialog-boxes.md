---
title: 创建和管理模式对话框|Microsoft Docs
description: 了解如何使用 DialogWindow 和 DialogWindow 在 Visual Studio内创建模式对话框。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- dialog boxes, managing in Visual Studio
ms.assetid: 491bc0de-7dba-478c-a76b-923440e090f3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 88c1f943fd7c8579673047acbc533ca4577992bc7e13258276496a2499129e5c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121293451"
---
# <a name="create-and-manage-modal-dialog-boxes"></a>创建和管理模式对话框
在 Visual Studio 内创建模式对话框时，必须确保对话框的父窗口在显示对话框时处于禁用状态，然后在对话框关闭后重新启用父窗口。 如果不这样做，可能会收到以下错误：Microsoft Visual Studio模式对话处于活动状态，因此无法 *关闭。关闭活动对话框，然后重试。*

有两种方法可以执行此操作。 如果具有 WPF 对话框，则建议从 派生该对话框，然后调用 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow.ShowModal%2A> 以显示该对话框。 如果这样做，则无需管理父窗口的模式状态。

如果对话框不是 WPF，或者由于某种其他原因无法从 派生对话框类，则必须通过调用 并自己管理模式状态来获取对话框的父级，方法是调用参数为 (false) 的 方法，然后显示对话框，然后在关闭对话框后再次调用参数为 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.GetDialogOwnerHwnd%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.EnableModeless%2A> 1 (true) 的 方法。

## <a name="create-a-dialog-box-derived-from-dialogwindow"></a>创建派生自 DialogWindow 的对话框

1. 创建名为 **OpenDialogTest** 的 VSIX 项目，并添加名为 **OpenDialog 的菜单命令**。 若要详细了解如何这样做，请参阅 [使用菜单命令 创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 若要使用 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> 类，必须在"添加引用"对话框的 ("框架"选项卡中添加对以下程序集) ： 

    - *PresentationCore*

    - *PresentationFramework*

    - *WindowsBase*

    - *System.Xaml*

3. 在 *OpenDialog.cs* 中，添加以下 `using` 语句：

    ```csharp
    using Microsoft.VisualStudio.PlatformUI;
    ```

4. 声明一个名为 `TestDialogWindow` 的类，该类派生自 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> ：

    ```csharp
    class TestDialogWindow : DialogWindow
    {. . .}
    ```

5. 若要能够最小化和最大化对话框，将 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMaximizeButton%2A> 和 设置为 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMinimizeButton%2A> true：

    ```csharp
    internal TestDialogWindow()
    {
        this.HasMaximizeButton = true;
        this.HasMinimizeButton = true;
    }
    ```

6. 在 `OpenDialog.ShowMessageBox` 方法中，将现有代码替换为以下内容：

    ```csharp
    TestDialogWindow testDialog = new TestDialogWindow();
    testDialog.ShowModal();
    ```

7. 生成并运行应用程序。 应显示 Visual Studio实例。 在实验 **实例** 的"工具"菜单上，应会看到名为 **"调用 OpenDialog"的命令**。 单击此命令时，应会看到对话框窗口。 你应该能够最小化和最大化窗口。

## <a name="create-and-manage-a-dialog-box-not-derived-from-dialogwindow"></a>创建和管理不是从 DialogWindow 派生的对话框

1. 对于此过程，可以使用在上一过程中创建的 **OpenDialogTest** 解决方案，并使用相同的程序集引用。

2. 添加以下 `using` 声明：

    ```csharp
    using System.Windows;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    ```

3. 创建一个名为 `TestDialogWindow2` 的类，该类派生自 <xref:System.Windows.Window> ：

    ```csharp
    class TestDialogWindow2 : Window
    {. . .}
    ```

4. 添加对 的专用引用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> ：

    ```
    private IVsUIShell shell;
    ```

5. 添加一个构造函数，用于将引用设置到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> ：

    ```csharp
    public TestDialogWindow2(IVsUIShell uiShell)
    {
        shell = uiShell;
    }
    ```

6. 在 `OpenDialog.ShowMessageBox` 方法中，将现有代码替换为以下内容：

    ```csharp
    IVsUIShell uiShell = (IVsUIShell)ServiceProvider.GetService(typeof(SVsUIShell));

    TestDialogWindow2 testDialog2 = new TestDialogWindow2(uiShell);
    //get the owner of this dialog
    IntPtr hwnd;
    uiShell.GetDialogOwnerHwnd(out hwnd);
    testDialog2.WindowStartupLocation = System.Windows.WindowStartupLocation.CenterOwner;
    uiShell.EnableModeless(0);
    try
    {
        WindowHelper.ShowModal(testDialog2, hwnd);
    }
    finally
    {
        // This will take place after the window is closed.
        uiShell.EnableModeless(1);
    }
    ```

7. 生成并运行应用程序。 在" **工具"** 菜单上，应会看到名为 **"调用 OpenDialog"的命令**。 单击此命令时，应会看到对话框窗口。
