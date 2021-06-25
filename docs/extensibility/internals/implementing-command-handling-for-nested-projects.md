---
title: 实现嵌套项目的命令处理 |Microsoft Docs
description: 了解如何在 Visual Studio 集成开发环境 (IDE) 中实现嵌套项目的命令处理。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- nested projects, implementing command handling
ms.assetid: 48a9d66e-d51c-4376-a95a-15796643a9f2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4324e207d7b424295137f9523ed0bed538b3d806
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899981"
---
# <a name="implementing-command-handling-for-nested-projects"></a>实现嵌套项目的命令处理
IDE 可以将通过和接口传递的命令传递 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 到嵌套项目，也可以使用父项目来筛选或重写命令。

> [!NOTE]
> 只能筛选父项目通常处理的命令。 不能对 IDE 处理的命令（如 " **生成** " 和 " **部署** "）进行筛选。

 以下步骤描述了实现命令处理的过程。

## <a name="procedures"></a>过程

#### <a name="to-implement-command-handling"></a>实现命令处理

1. 当用户选择嵌套项目或嵌套项目中的节点时：

   1. IDE 将调用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法。

      — 或 —

   2. 如果命令源自层次结构窗口（如解决方案资源管理器中的快捷菜单命令），IDE 将对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> 项目的父项调用方法。

2. 父项目可以检查要传递到 `QueryStatus` 的参数（例如 `pguidCmdGroup` 和）， `prgCmds` 以确定父项目是否应筛选命令。 如果为筛选命令实现了父项目，则应将其设置为：

   ```
   prgCmds[0].cmdf = OLECMDF_SUPPORTED;
   // make sure it is disabled
   prgCmds[0].cmdf &= ~MSOCMDF_ENABLED;
   ```

    然后，父项目应返回 `S_OK` 。

    如果父项目未筛选此命令，则它应该只返回 `S_OK` 。 在这种情况下，IDE 会自动将命令路由到子项目。

    父项目不需要将命令路由到子项目。 IDE 将执行此任务。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)
- [嵌套项目](../../extensibility/internals/nesting-projects.md)
