---
title: 使用互操作程序集的命令和菜单 |Microsoft Docs
description: 了解通过使用互操作程序集实现 VSPackage 中的菜单和工具栏命令时必须完成的任务。
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
ms.openlocfilehash: 0198490f6792654a95e9bea0f2b270dadd85a17e959a9817e0f74165a14a11bd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432639"
---
# <a name="commands-and-menus-that-use-interop-assemblies"></a>使用互操作程序集的命令和菜单
使用互操作程序集实现菜单和工具栏命令的 VSPackage 必须：

- 通知 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集成开发环境 (IDE) 它支持的命令以及它们当前是否已启用。

- 遵循用于处理命令 (约定) 的规则。

- 使用或接口显式实现命令处理 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 。

  以下部分介绍如何执行这些任务。

## <a name="in-this-section"></a>本节内容
- [使用互操作程序集确定命令状态](../../extensibility/internals/determining-command-status-by-using-interop-assemblies.md)

 介绍 VSPackage 如何通知 IDE 它所支持的命令以及它们当前是否已启用。

- [互操作程序集中的命令约定](../../extensibility/internals/command-contracts-in-interop-assemblies.md)

 提供使用互操作程序集的所有 Vspackage 实现命令所使用的基本命令协定的定义。

- [命令实现](../../extensibility/internals/command-implementation.md)

 概述 VSPackage 如何实现命令。

- [注册互操作程序集命令处理程序](../../extensibility/internals/registering-interop-assembly-command-handlers.md)

 描述通知 IDE VSPackage 提供命令处理程序所需的注册表项。

## <a name="related-sections"></a>相关章节
- [命令可用性](../../extensibility/internals/command-availability.md)

 描述 IDE 使用哪些条件来确定哪些 VSPackage 命令可用以及哪些对象处理它们。

- [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 提供有关如何创建使用命令支持的 UI 的详细信息 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [Vspackage 中的命令传送](../../extensibility/internals/command-routing-in-vspackages.md)

 使用正确的命令请求将对象与对象相关联的过程的概述。
