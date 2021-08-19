---
title: 为嵌套项目实现命令处理|Microsoft Docs
description: 了解如何在 IDE Visual Studio 集成开发环境中为嵌套项目 (命令) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- nested projects, implementing command handling
ms.assetid: 48a9d66e-d51c-4376-a95a-15796643a9f2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 9489f37fff9fe1e798a42825a29cf59ec49336e2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122042317"
---
# <a name="implementing-command-handling-for-nested-projects"></a>实现嵌套项目的命令处理
IDE 可以将通过 和 接口传递的命令传递给嵌套项目，或者 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 父项目可以筛选或替代这些命令。

> [!NOTE]
> 只能筛选通常由父项目处理的命令。 无法筛选 **由** IDE 处理的 **生成** 和部署等命令。

 以下步骤介绍了实现命令处理的过程。

## <a name="procedures"></a>过程

#### <a name="to-implement-command-handling"></a>实现命令处理

1. 当用户选择嵌套项目或嵌套项目中的节点时：

   1. IDE 调用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法。

      — 或 —

   2. 如果命令源自层次结构窗口（如 解决方案资源管理器 中的快捷菜单命令）中，则 IDE 将调用项目父级上的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> 方法。

2. 父项目可以检查要传递给 的参数，如 和 `QueryStatus` `pguidCmdGroup` ，以确定 `prgCmds` 父项目是否应该筛选命令。 如果实现父项目以筛选命令，则它应设置：

   ```
   prgCmds[0].cmdf = OLECMDF_SUPPORTED;
   // make sure it is disabled
   prgCmds[0].cmdf &= ~MSOCMDF_ENABLED;
   ```

    然后，父项目应返回 `S_OK` 。

    如果父项目不筛选命令，则它只应返回 `S_OK` 。 在这种情况下，IDE 会自动将命令路由到子项目。

    父项目无需将命令路由到子项目。 IDE 执行此任务。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)
- [嵌套项目](../../extensibility/internals/nesting-projects.md)
