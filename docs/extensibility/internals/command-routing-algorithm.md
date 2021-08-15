---
title: 命令路由算法|Microsoft Docs
description: 了解命令解析的顺序Visual Studio因为命令由不同的组件处理，并且从最内层路由到最外层上下文。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, routing
- command routing
ms.assetid: 998b616b-bd08-45cb-845f-808efb8c33bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 4749aba212a2ec8547d93cb48b0090908c9959fc01fe11fd8e1b582e4da76aa3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448242"
---
# <a name="command-routing-algorithm"></a>命令路由算法
在Visual Studio命令由许多不同的组件处理。 命令从最内部的上下文（基于当前选择）路由到最外层 (也称为全局) 上下文。 有关详细信息，请参阅命令 [可用性](../../extensibility/internals/command-availability.md)。

## <a name="order-of-command-resolution"></a>命令解析顺序
 命令通过以下级别的命令上下文传递：

1. 外接程序：环境首先向存在的任何外接程序提供 命令。

2. 优先级命令：这些命令是使用 注册的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget> 。 它们针对每个命令Visual Studio调用，并按其注册顺序调用。

3. 上下文菜单命令：位于上下文菜单上的命令首先提供给提供给上下文菜单的命令目标，之后提供给典型路由。

4. 工具栏集命令目标：调用 时，将注册这些命令目标 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell4.SetupToolbar2%2A> 。 参数 `pCmdTarget` 可以是 `null` 。 如果不是 ， `null` 则此命令目标用于更新位于正在设置的工具栏上的任何命令。 如果 shell 正在设置工具栏，它会将窗口框架作为 传递，以便工具栏上命令的所有更新都流经窗口框架，即使它不在焦点 `pCmdTarget` 中。

5. 工具窗口：通常实现 接口的工具窗口还应实现 接口，以便Visual Studio窗口处于活动状态时获取 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 命令目标。 但是，如果具有焦点的工具窗口是Project窗口，则命令将路由到作为所选项的常见 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 父级的接口。 如果此选择跨多个项目，则命令将路由到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> 层次结构。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>接口包含 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> 方法，这些方法类似于 接口上的相应 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 命令。

6. 文档窗口：如果命令的 .vsct 文件中设置了 标志，Visual Studio 将查找文档视图对象上的命令目标，该对象是接口的实例或文档对象的实例 (通常是接口或接口 `RouteToDocs`  <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>) 。 如果文档视图对象不支持该命令，Visual Studio命令路由到 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 返回的接口。  (这是文档数据对象的可选接口。) 

7. 当前层次结构：当前层次结构可以是拥有活动文档窗口的项目，或者是在 **解决方案资源管理器。** Visual Studio查找在当前层次结构或活动层次结构 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 上实现的接口。 层次结构应支持在层次结构处于活动状态时有效的命令，即使项目项的文档窗口具有焦点。 但是，只有在具有焦点 **解决方案资源管理器** 才能使用 接口及其 和 方法支持 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 应用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> 的命令。

     **剪切**、**复制、****粘贴****、删除、****重命名****、输入** 和 **DoubleClick** 命令需要特殊处理。 有关如何处理层次结构中的 **Delete** 和 **Remove** 命令的信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler> 接口。

8. 全局：如果前面提到的上下文尚未处理命令，Visual Studio尝试将其路由到拥有实现 接口的命令的 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> VSPackage。 如果尚未加载 VSPackage，则调用 方法Visual Studio加载 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 它。 VSPackage 仅在调用 方法 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 时加载。

## <a name="see-also"></a>另请参阅
- [命令设计](../../extensibility/internals/command-design.md)
