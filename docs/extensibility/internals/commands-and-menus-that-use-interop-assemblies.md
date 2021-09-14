---
title: 使用互操作程序集命令和菜单|Microsoft Docs
description: 了解在使用互操作程序集在 VSPackage 中实现菜单和工具栏命令时必须完成的任务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, using interop assemblies
- interop assemblies, using in commands and menus
- commands, handling using interop assemblies
- command handling with interop assemblies
ms.assetid: 8f4af525-39e5-4e69-92c8-d3efabe80bb2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 12f6cd61eb7e5f3e6bc96722f8d2ad8f29f5ee97
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602588"
---
# <a name="commands-and-menus-that-use-interop-assemblies"></a>使用互操作程序集的命令和菜单
使用互操作程序集实现菜单和工具栏命令的 VSPackage 必须：

- 通知 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集成开发环境 (IDE) 其支持的命令以及它们当前是否已启用。

- 遵循用于处理命令 (协定) 规则。

- 使用 或 接口显式实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 命令 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 处理。

  以下部分介绍如何执行这些任务。

## <a name="in-this-section"></a>本节内容
- [使用互操作程序集确定命令状态](../../extensibility/internals/determining-command-status-by-using-interop-assemblies.md)

 描述 VSPackage 如何通知 IDE 它支持哪些命令，以及它们当前是否已启用。

- [互操作程序集中的命令协定](../../extensibility/internals/command-contracts-in-interop-assemblies.md)

 提供使用互操作程序集实现命令的所有 VSPackage 使用的基本命令协定的定义。

- [命令实现](../../extensibility/internals/command-implementation.md)

 概述 VSPackage 如何实现命令。

- [注册互操作程序集命令处理程序](../../extensibility/internals/registering-interop-assembly-command-handlers.md)

 描述通知 IDE VSPackage 提供命令处理程序所需的注册表项。

## <a name="related-sections"></a>相关章节
- [命令可用性](../../extensibility/internals/command-availability.md)

 描述 IDE 用于确定哪些 VSPackage 命令可用以及哪些对象处理这些命令的条件。

- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 提供有关如何创建使用命令支持的 UI [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的详细信息。

- [VSPackages 中的命令路由](../../extensibility/internals/command-routing-in-vspackages.md)

 概述用于将对象与正确的命令请求关联的过程。
