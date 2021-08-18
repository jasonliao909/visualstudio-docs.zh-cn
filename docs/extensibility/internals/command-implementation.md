---
title: 命令实现|Microsoft Docs
description: 了解如何在 Visual Studio中实现命令、如何在 VSPackage 中设置命令组、向它添加命令、注册命令以及实现该命令。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, implementation
ms.assetid: c782175c-cce4-4bd0-8374-4a897ceb1b3d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 76cb43ec2df05480563f0f7f70e1e4fbecbf44c2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122095018"
---
# <a name="command-implementation"></a>命令实现
若要在 VSPackage 中实现命令，必须执行以下任务：

1. 在 *.vsct* 文件中，设置一个命令组，然后将命令添加到它。 有关详细信息，请参阅命令[Visual Studio表 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

2. 将命令注册到 Visual Studio。

3. 实现 命令。

以下部分介绍如何注册和实现命令。

## <a name="register-commands-with-visual-studio"></a>将命令注册到Visual Studio
 如果命令将显示在菜单上，则必须将 添加到 VSPackage，并使用 作为菜单名称或资源 <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> ID 的值。

```
[ProvideMenuResource("Menus.ctmenu", 1)]
...
    public sealed class MyPackage : Package
    {.. ..}

```

 此外，还必须将 命令注册到 <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> 。 如果 VSPackage 派生自 ，可以使用 方法 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 获取此服务 <xref:Microsoft.VisualStudio.Shell.Package> 。

```
OleMenuCommandService mcs = GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
if ( null != mcs )
{
    // Create the command for the menu item.
    CommandID menuCommandID = new CommandID(guidCommandGroup, myCommandID);
    MenuCommand menuItem = new MenuCommand(MenuItemCallback, menuCommandID );
    mcs.AddCommand( menuItem );
}

```

## <a name="implement-commands"></a>实现命令
 有许多方法可以实施命令。 如果需要静态菜单命令（一个始终以相同方式显示的命令，并在同一菜单上显示该命令，则使用 创建命令，如上一部分 <xref:System.ComponentModel.Design.MenuCommand> 的示例所示。 若要创建静态命令，必须提供负责执行该命令的事件处理程序。 由于命令始终启用且可见，因此不需要提供其状态来Visual Studio。 如果要根据特定条件更改命令的状态，可以创建命令作为 类的实例，并在其构造函数中提供一个事件处理程序来执行该命令，并提供一个处理程序以在命令状态更改时通知 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> `QueryStatus` Visual Studio。 还可以作为命令类的一部分实现 ，或者，如果要在项目中提供命令， <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 则还可以实现 。 这两个接口和 类均具有通知Visual Studio状态更改的方法，以及提供命令执行的其他 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 方法。

 将命令添加到命令服务后，它将成为命令链之一。 为命令实现状态通知和执行方法时，请注意仅提供该特定命令，以及将所有其他事例传递给链中的其他命令。 如果无法将命令传递给 (通常返回 <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>) ，Visual Studio可能会停止正常工作。

## <a name="querystatus-methods"></a>QueryStatus 方法
 如果要实现 方法或 方法，请检查命令所属的命令集的 GUID 和命令 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> 的 ID。 请遵循这些指导：

- 如果无法识别 GUID，则任一方法的实现都必须返回 <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP> 。

- 如果任一方法的实现能够识别 GUID，但尚未实现命令，则该方法应返回 <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> 。

- 如果任一方法的实现同时识别 GUID 和 命令，则 方法应设置 参数中每个命令 (的命令标志字段) 标志 `prgCmds` <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> ：

  - `OLECMDF_SUPPORTED`：支持 命令。

  - `OLECMDF_INVISIBLE`：该命令不应可见。

  - `OLECMDF_LATCHED`：命令已打开，似乎已选中。

  - `OLECMDF_ENABLED`：命令已启用。

  - `OLECMDF_DEFHIDEONCTXTMENU`：如果命令显示在快捷菜单上，应隐藏该命令。

  - `OLECMDF_NINCHED`：该命令是菜单控制器，未启用，但其下拉菜单列表不为空，并且仍然可用。  (很少使用此标志。) 

- 如果在带 标志的 *.vsct* 文件中定义了命令， `TextChanges` 请设置以下参数：

  - 将 `rgwz` 参数的 `pCmdText` 元素设置为命令的新文本。

  - 将 `cwActual` 参数的 `pCmdText` 元素设置为命令字符串的大小。

此外，请确保当前上下文不是自动化函数，除非命令专门用于处理自动化函数。

若要指示支持特定命令，请返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 。 对于所有其他命令，返回 <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> 。

在下面的示例中， 方法首先确保上下文不是自动化函数，然后查找正确的命令集 `QueryStatus` GUID 和命令 ID。 命令本身设置为启用和支持。 不支持其他命令。

```csharp
public int QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)
{
    if (!VsShellUtilities.IsInAutomationFunction(m_provider.ServiceProvider))
    {
        if (pguidCmdGroup == VSConstants.VSStd2K && cCmds > 0)
        {
            // make the Right command visible
            if ((uint)prgCmds[0].cmdID == (uint)VSConstants.VSStd2KCmdID.RIGHT)
            {
                prgCmds[0].cmdf = (int)Microsoft.VisualStudio.OLE.Interop.Constants.MSOCMDF_ENABLED | (int)Microsoft.VisualStudio.OLE.Interop.Constants.MSOCMDF_SUPPORTED;
                return VSConstants.S_OK;
            }
        }
        return Constants.OLECMDERR_E_NOTSUPPORTED;
    }
}
```

## <a name="execution-methods"></a>执行方法
 方法的 `Exec` 实现类似于 方法的 `QueryStatus` 实现。 首先，请确保上下文不是自动化函数。 然后，测试 GUID 和命令 ID。 如果无法识别 GUID 或命令 ID，则返回 <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> 。

 若要处理命令，请执行该命令，如果 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 执行成功，则返回 。 命令负责错误检测和通知;因此，如果执行失败，则返回错误代码。 下面的示例演示如何实现执行方法。

```csharp
public int Exec(ref Guid pguidCmdGroup, uint nCmdID, uint nCmdexecopt, IntPtr pvaIn, IntPtr pvaOut)
{
    if (!VsShellUtilities.IsInAutomationFunction(m_provider.ServiceProvider))
    {
        if (pguidCmdGroup == VSConstants.GUID_VSStandardCommandSet97)
        {
             if (nCmdID ==(uint) uint)VSConstants.VSStd2KCmdID.RIGHT)
            {
                //execute the command
                return VSConstants.S_OK;
            }
        }
    }
    return Constants.OLECMDERR_E_NOTSUPPORTED;
}
```

## <a name="see-also"></a>请参阅

- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
