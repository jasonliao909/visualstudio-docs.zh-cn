---
title: 命令传送算法 |Microsoft Docs
description: 了解 Visual Studio 中的命令解析顺序，因为命令由不同组件处理，并从最内部到最外层上下文。
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
ms.openlocfilehash: f99b4e8a4f883d752d217bb1859822c65af07116
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665335"
---
# <a name="command-routing-algorithm"></a>命令传送算法
在 Visual Studio 命令由许多不同的组件进行处理。 命令从最内层的上下文路由，该上下文基于当前所选内容，到最外面的 (（也称为全局) 上下文）。 有关详细信息，请参阅 [命令可用性](../../extensibility/internals/command-availability.md)。

## <a name="order-of-command-resolution"></a>命令解析顺序
 命令通过以下命令上下文级别传递：

1. 外接程序：环境首先向存在的任何外接程序提供命令。

2. 优先级命令：这些命令是使用注册的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget> 。 它们是为 Visual Studio 中的每个命令调用的，并按它们的注册顺序进行调用。

3. 上下文菜单命令：位于上下文菜单上的命令首先向向上下文菜单提供的命令目标提供，并在该位置之后提供给典型路由。

4. 工具栏设置命令目标：调用时注册这些命令目标 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell4.SetupToolbar2%2A> 。 `pCmdTarget`参数可以是 `null` 。 如果不是 `null` ，则使用此命令 target 来更新位于所设置的工具栏上的所有命令。 如果 shell 设置了工具栏，则会将窗口框架作为传递， `pCmdTarget` 以便对工具栏上的命令进行的所有更新都流过窗口框架，即使未处于焦点状态也是如此。

5. 工具窗口：工具窗口通常实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> 接口，还应实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口，以便在工具窗口为活动窗口时 Visual Studio 可以获取命令目标。 但是，如果具有焦点的工具窗口是 **Project** 窗口，则该命令将路由到作为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 所选项的公共父对象的接口。 如果此选择跨多个项目，则将命令路由到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> 层次结构。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>接口包含 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> 与 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> 接口上的相应命令相似的和方法 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。

6. "文档窗口"：如果命令在 `RouteToDocs` *.vsct* 文件中设置了标志，Visual Studio 将在文档视图对象上查找命令目标，该对象既可以是接口的实例， <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> 也可以是文档对象的实例， (通常是 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> 接口或 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>) 接口。 如果文档视图对象不支持该命令，Visual Studio 会将命令路由到返回的 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口。  (这是文档数据对象的可选接口。 ) 

7. 当前层次结构：当前层次结构可以是拥有活动文档窗口的项目，也可以是在 **解决方案资源管理器** 中选择的层次结构。 Visual Studio 查找 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 在当前或活动层次结构上实现的接口。 层次结构应支持在层次结构处于活动状态时有效的命令，即使项目项的文档窗口具有焦点也是如此。 但是，仅当 **解决方案资源管理器** 具有焦点时，才必须使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 接口及其 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> 和方法来支持命令 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> 。

     **剪切**、 **复制**、 **粘贴**、 **删除**、 **重命名**、 **输入** 和 **DoubleClick** 命令需要特殊处理。 有关如何处理层次结构中 **删除** 和 **删除** 命令的信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler> 接口。

8. 全局：如果命令尚未由前面提到的上下文处理，Visual Studio 会尝试将其路由到拥有实现接口的命令的 VSPackage <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。 如果尚未加载 VSPackage，则在 Visual Studio 调用方法时不会加载它 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 。 VSPackage 仅在调用方法时加载 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 。

## <a name="see-also"></a>另请参阅
- [命令设计](../../extensibility/internals/command-design.md)
