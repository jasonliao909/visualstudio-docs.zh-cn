---
title: 创建多实例工具窗口|Microsoft Docs
description: 了解如何修改工具窗口，以便可以同时打开该工具窗口的多个实例。 默认情况下，工具窗口只能打开一个实例。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- multi
- tool windows
ms.assetid: 4a7872f1-acc9-4f43-8932-5a526b36adea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 61b9f21163fd9382575aa97693e955a5cf710b6e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600990"
---
# <a name="create-a-multi-instance-tool-window"></a>创建多实例工具窗口
可以编程工具窗口，以便可以同时打开它的多个实例。 默认情况下，工具窗口只能打开一个实例。

使用多实例工具窗口时，可以同时显示多个相关信息源。 例如，你可以将多行控件放在多实例工具窗口中，以便多个代码片段在编程会话 <xref:System.Windows.Forms.TextBox> 期间同时可用。 此外，例如，可以将控件和下拉列表框放在多实例工具窗口中，以便可以同时跟踪多个实时 <xref:System.Windows.Forms.DataGrid> 数据源。

## <a name="create-a-basic-single-instance-tool-window"></a>创建一个基本 (单实例) 工具窗口

1. 使用 VSIX 模板创建名为 **MultiInstanceToolWindow** 的项目，并添加名为 **MIToolWindow** 的自定义工具窗口项模板。

    > [!NOTE]
    > 有关使用工具窗口创建扩展的信息，请参阅使用工具窗口 [创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

## <a name="make-a-tool-window-multi-instance"></a>使工具窗口成为多实例

1. 打开 *MIToolWindowPackage.cs* 文件并找到 `ProvideToolWindow` 属性。 和 `MultiInstances=true` 参数，如以下示例所示：

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
        [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
        [ProvideMenuResource("Menus.ctmenu", 1)]
        [ProvideToolWindow(typeof(MultiInstanceToolWindow.MIToolWindow), MultiInstances = true)]
        [Guid(MIToolWindowPackage.PackageGuidString)]
        public sealed class MIToolWindowPackage : Package
    {. . .}
    ```

2. 在 *MIToolWindowCommand.cs* 文件中，找到 `ShowToolWindos()` 方法。 在此方法中，调用 方法，并设置其 标志，以便它将通过现有工具窗口实例进行访问，直到找到 <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> `create` 可用的 `false` `id` 。

3. 若要创建工具窗口实例，请调用 <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> 方法，将方法设置为 `id` 可用值，将 标志 `create` 设置为 `true` 。

    默认情况下， 方法 `id` 的 参数 <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> 的值为 `0` 。 此值将创建单实例工具窗口。 若要托管多个实例，每个实例都必须具有自己唯一的 `id` 。

4. 对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> 工具窗口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> 实例的 属性返回的 对象调用 <xref:Microsoft.VisualStudio.Shell.ToolWindowPane.Frame%2A> 方法。

5. 默认情况下， `ShowToolWindow` 由工具窗口项模板创建的方法将创建单实例工具窗口。 下面的示例演示如何修改 方法 `ShowToolWindow` 以创建多个实例。

    ```csharp
    private void ShowToolWindow(object sender, EventArgs e)
    {
        for (int i = 0; i < 10; i++)
        {
            ToolWindowPane window = this.package.FindToolWindow(typeof(MIToolWindow), i, false);
            if (window == null)
            {
                // Create the window with the first free ID.
                window = (ToolWindowPane)this.package.FindToolWindow(typeof(MIToolWindow), i, true);
                if ((null == window) || (null == window.Frame))
                {
                    throw new NotSupportedException("Cannot create tool window");
                }

            IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;
            Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());
            break;
            }
        }
    }
    ```
