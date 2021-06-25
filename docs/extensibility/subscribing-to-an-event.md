---
title: 订阅事件|Microsoft Docs
description: 了解如何创建一个工具窗口，用于响应 Visual Studio SDK 中正在运行的文档表中的事件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- running document table (RDT), responding to events
- running document table (RDT), subscribing to events
ms.assetid: e94a4fea-94df-488e-8560-9538413422bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 01271016eed9a4a157b333a2f0435589b0a028d5
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899382"
---
# <a name="subscribing-to-an-event"></a>订阅事件
本演练介绍如何创建一个工具窗口，用于响应 RDT (中正在运行的文档) 。 工具窗口承载实现 的用户控件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> 。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A>方法将 接口连接到 事件。

## <a name="prerequisites"></a>先决条件
 从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装 Visual Studio [SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="subscribing-to-rdt-events"></a>订阅 RDT 事件

#### <a name="to-create-an-extension-with-a-tool-window"></a>使用工具窗口创建扩展

1. 使用 VSIX 模板创建名为 **RDTExplorer** 的项目，并添加名为 **RDTExplorerWindow** 的自定义工具窗口项模板。

     有关使用工具窗口创建扩展的信息，请参阅 [使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

#### <a name="to-subscribe-to-rdt-events"></a>订阅 RDT 事件

1. 打开 RDTExplorerWindowControl.xaml 文件并删除名为 的按钮 `button1` 。 添加 <xref:System.Windows.Forms.ListBox> 控件并接受默认名称。 Grid 元素应如下所示：

    ```xml
    <Grid>
        <StackPanel Orientation="Vertical" Margin="-10,10,10,0">
            <TextBlock Margin="10" HorizontalAlignment="Center">RDTExplorerWindow</TextBlock>
            <ListBox x:Name="listBox" Height="100" />
        </StackPanel>
    </Grid>
    ```

2. 在代码视图中打开 RDTExplorerWindow.cs 文件。 将以下 using 指令添加到文件的起始位置。

    ```csharp
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

3. 修改 `RDTExplorerWindow` 类，以便除了从 类派生之外 <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> ，它还实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> 接口。

    ```csharp
    public class RDTExplorerWindow : ToolWindowPane, IVsRunningDocTableEvents
    {. . .}
    ```

4. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>。

    - 实现 接口。 将光标置于 IVsRunningDocTableEvents 名称上。 应在左边距看到一个灯泡。 单击灯泡右边的向下箭头，然后选择"实现 **接口"。**

5. 在 接口的每个方法中，将 行 `throw new NotImplementedException();` 替换为以下代码：

    ```csharp
    return VSConstants.S_OK;
    ```

6. 将 Cookie 字段添加到 RDTExplorerWindow 类。

    ```csharp
    private uint rdtCookie;
    ```

     这保存方法返回的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> Cookie。

7. 重写 RDTExplorerWindow 的 Initialize () 以注册 RDT 事件。 应始终在 ToolWindowPane 的 Initialize () 方法（而不是构造函数）获取服务。

    ```csharp
    protected override void Initialize()
    {
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)
        this.GetService(typeof(SVsRunningDocumentTable));
        rdt.AdviseRunningDocTableEvents(this, out rdtCookie);
    }
    ```

     <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>调用服务以获取 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> 接口。 方法将 RDT 事件连接到实现 的对象（本 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> 例中为 RDTExplorer 对象）。

8. 更新 RDTExplorerWindow 的 Dispose () 方法。

    ```csharp
    protected override void Dispose(bool disposing)
    {
        // Release the RDT cookie.
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)
            Package.GetGlobalService(typeof(SVsRunningDocumentTable));
        rdt.UnadviseRunningDocTableEvents(rdtCookie);

        base.Dispose(disposing);
    }
    ```

     <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnadviseRunningDocTableEvents%2A>方法删除 和 `RDTExplorer` RDT 事件通知之间的连接。

9. 将以下行添加到处理程序的正文中， <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnBeforeLastDocumentUnlock%2A> 就在 `return` 语句之前。

    ```csharp
    public int OnBeforeLastDocumentUnlock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)
    {
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnBeforeLastDocumentUnlock");
        return VSConstants.S_OK;
    }
    ```

10. 将类似的行添加到处理程序的正文和想要在列表框中 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterFirstDocumentLock%2A> 看到的其他事件。

    ```csharp
    public int OnAfterFirstDocumentLock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)
    {
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnAfterFirstDocumentLock");
        return VSConstants.S_OK;
    }
    ```

11. 生成项目并启动调试。 将显示Visual Studio实例。

12. 打开 **RDTExplorerWindow** (**视图/ 其他 Windows / RDTExplorerWindow**) 。

     **RDTExplorerWindow 窗口** 随即打开，其中显示一个空事件列表。

13. 打开或创建解决方案。

     触发 `OnBeforeLastDocument` `OnAfterFirstDocument` 和 事件时，事件列表中会显示每个事件的通知。
