---
title: 命令设计|Microsoft Docs
description: 了解如何在 Visual Studio 中为 VSPackage 设计命令。 包括如何指定其显示位置、可用时间以及处理方式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands
- commands, implementation
ms.assetid: 097108c3-f758-4b87-89d6-b32d12d9041a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 48b438f457dea5aad5c241b0fd1e60daac3761a2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110561"
---
# <a name="command-design"></a>命令设计
将命令添加到 VSPackage 时，必须指定命令的显示位置、可用时间以及处理方式。

## <a name="define-commands"></a>定义命令
 若要定义新命令，请Visual Studio VSPackage (*.vsct*) 文件。 如果已使用 Visual Studio 模板创建了 VSPackage，则项目将包含这些文件之一。 有关详细信息，请参阅命令[Visual Studio表 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

 Visual Studio合并找到的所有 *.vsct* 文件，以便可以显示命令。 由于这些文件与 VSPackage 二进制文件Visual Studio，因此无需加载包来查找命令。 有关详细信息，请参阅 [VSPackages 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)。

 Visual Studio注册 <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> 属性来定义菜单资源和命令。 有关详细信息，请参阅命令 [实现](../../extensibility/internals/command-implementation.md)。

 可以以多种不同方式运行时更改命令。 可以显示或隐藏、启用或禁用它们。 它们可以显示不同的文本或图标，也可以包含不同的值。 在加载 VSPackage 之前，可能会Visual Studio大量自定义。 有关详细信息，请参阅 [VSPackages 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)。

## <a name="command-handlers"></a>命令处理程序
 创建命令时，必须提供事件处理程序来执行该命令。 如果用户选择命令，则必须正确路由该命令。 路由命令意味着将其发送到正确的 VSPackage 以启用或禁用它，隐藏或显示该命令，如果用户选择这样做，则执行该命令。 有关详细信息，请参阅命令 [路由算法](../../extensibility/internals/command-routing-algorithm.md)。

## <a name="visual-studio-command-environment"></a>Visual Studio命令环境
 Visual Studio可以托管任意数目的 VSPackage，并且每个都可以提供自己的命令集。 环境仅显示适用于当前任务的命令。 有关详细信息，请参阅命令[可用性和](../../extensibility/internals/command-availability.md)[选择上下文对象](../../extensibility/internals/selection-context-objects.md)。

 定义新命令、菜单、工具栏或快捷菜单的 VSPackage 在安装时通过引用本机或托管程序集中的资源的注册表项Visual Studio向 Visual Studio 提供其命令信息。 然后，每个资源引用一个二进制数据资源 (*.cto*) 文件，该文件是在编译 Visual Studio 命令表 (*.vsct*) 时生成的。 这使Visual Studio提供合并的命令集、菜单和工具栏，而无需加载每个已安装的 VSPackage。

### <a name="command-organization"></a>命令组织
 环境按组、优先级和菜单定位命令。

- 组是相关命令的逻辑集合，例如剪切、**复制** 和 **粘贴命令** 组。 组是菜单上显示的命令。

- 优先级确定组中单个命令在菜单上的显示顺序。

- 菜单充当组的容器。

  环境预先定义一些命令、组和菜单。 有关详细信息，请参阅默认 [命令、组和工具栏位置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)。

  可以将命令分配给主组。 主组控制命令在主菜单结构和"自定义"对话框中的位置。  命令可以出现在多个组中;例如，命令可以位于主菜单、快捷菜单和工具栏上。 有关详细信息，请参阅 [VSPackages 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)。

### <a name="command-routing"></a>命令路由
 为 VSPackage 调用和路由命令的过程与在对象实例上调用方法的过程不同。

 环境按顺序将命令从最 (本地) 命令上下文（基于当前选择）路由到最 (全局) 上下文。 能够执行命令的第一个上下文是处理该命令的上下文。 有关详细信息，请参阅命令 [路由算法](../../extensibility/internals/command-routing-algorithm.md)。

 在大多数情况下，环境使用 接口处理 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 命令。 由于命令路由方案允许许多不同的对象处理命令，因此可通过任意数目的对象实现;这些对象包括 Microsoft ActiveX 控件、窗口视图实现、文档对象、项目层次结构和 VSPackage 对象本身 (全局命令 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>) 。 在某些专用情况下（例如，在层次结构中路由命令） <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 中，必须实现 接口。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[命令实现](../../extensibility/internals/command-implementation.md)|介绍如何在 VSPackage 中实现命令。|
|[命令可用性](../../extensibility/internals/command-availability.md)|描述Visual Studio上下文如何确定哪些命令可用。|
|[命令路由算法](../../extensibility/internals/command-routing-algorithm.md)|描述Visual Studio路由体系结构如何允许不同的 VSPackage 处理命令。|
|[命令放置指南](../../extensibility/internals/command-placement-guidelines.md)|建议如何在安全环境中Visual Studio命令。|
|[VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)|描述 VSPackage 如何以最佳方式利用 Visual Studio体系结构。|
|[默认命令、组和工具栏位置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)|描述 VSPackage 如何以最佳方式使用这些命令中包含的Visual Studio。|
|[管理 VSPackage](../../extensibility/managing-vspackages.md)|介绍如何Visual Studio VSPackage。|
|[Visual Studio命令表 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)|提供有关基于 XML 的 *.vsct* 文件的信息，这些文件用于描述 VSPackage 中命令的布局和外观。|
