---
title: 自定义用户界面 (源代码管理 VSPackage) |Microsoft Docs
description: 了解如何通过使用源代码管理 VSPackage (UI 元素) 在 Visual Studio 中创建自定义用户界面。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interface, source control packages
- source control packages, user interface
ms.assetid: f35ddb24-53bf-461e-b34f-7414f657c082
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b688933859a4993b3032ab5b3fd1672eeae7261a4afb0788f5329435f12f98d7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121275510"
---
# <a name="custom-user-interface-source-control-vspackage"></a>自定义用户界面 (VSPackage) 
VSPackage 通过 *.vsct* Visual Studio 命令表声明其 (及其) 状态。 集成 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 开发环境 (IDE) 在加载 VSPackage 之前以默认状态显示菜单项。 随后，调用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法以启用或禁用菜单项。

 VSPackage 可以设置注册表项，以便根据命令用户界面 (UI) 上下文自动加载 VSPackage，尽管通常应按需加载源代码管理 VSPackage，而不是仅切换到特定的 UI 上下文。 有关 **AutoLoadPackages** 注册表项的信息，请参阅管理 [VSPackages](../../extensibility/managing-vspackages.md)。

## <a name="vspackage-ui"></a>VSPackage UI
 源代码管理包作为 VSPackage 实现，不使用 来自 的任何 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] UI。 每个源代码管理 VSPackage 都必须指定其自己的 UI 元素，例如菜单项、菜单组、工具窗口、工具栏，以及设置特定于源代码管理 VSPackage 的选项所需的任何 UI。 可以静态或动态启用这些 UI 元素。 静态 UI 元素在 *.vsct* 文件中定义，无论是否加载 VSPackage，都将显示这些元素。 动态 UI 元素可能可见，具体取决于特定的命令 UI 上下文（如 ）或作为对 方法 <xref:EnvDTE.Constants.vsContextNoSolution> 的 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 调用的结果。 动态 UI 元素的可见性符合延迟加载 VSPackage 的策略。

## <a name="ui-constraints-on-source-control-vspackages"></a>源代码管理 VSPackage 上的 UI 约束
 由于加载 IDE 后无法从 IDE 中删除源代码管理 VSPackage，因此 VSPackage 必须能够进入非活动状态。 当 VSPackage 收到其不再处于活动状态的通知时，VSPackage 将禁用其 UI 并忽略任何外部 IDE 交互。 VSPackage 的 方法实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 应在 VSPackage 不处于活动状态时隐藏命令。

 每个源代码管理 VSPackage 都必须实现 `IVsSccProvider` 接口。 接口上的两个方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> （ 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A> ）必须由 VSPackage 实现。

 源代码管理 VSPackage 可能订阅了各种 IDE 事件，这些事件由 、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> 等 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> 实现。 此外，VSPackage 可能实现了启用了注册表的回调接口，例如 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> 。 非活动时必须忽略这些接口。

 以下列表显示了受源代码管理 VSPackage 的活动状态影响的接口：

- 跟踪项目文档事件。

- 解决方案事件。

- 解决方案持久性接口。 处于非活动状态时，包不应写入 *.sln* 和 *.suo* 文件。

- 属性扩展程序。

  当源代码管理 VSPackage 处于非活动状态时，不会调用必需的 和 以及任何与源代码管理关联的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> 可选接口。

  启动 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 时，将命令 UI 上下文设置为当前默认源代码管理 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage ID 的 ID。 这会导致活动源代码管理 VSPackage 的静态 UI 出现在 IDE 中，而无需实际加载 VSPackage。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 暂停 VSPackage，使其在调用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage 之前通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider> 注册。

  下表介绍了有关 IDE 如何隐藏不同 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] UI 项的具体详细信息。

| UI 项 | 说明 |
| - | - |
| 菜单和工具栏 | 源代码管理包必须将初始菜单和工具栏可见性状态设置为 *.vsct* 文件的 [VisibilityConstraints](../../extensibility/visibilityconstraints-element.md)节中的源代码管理包 ID。 这使 IDE 可以适当地设置菜单项的状态，而无需加载 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage 并调用 方法的 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 实现。 |
| 工具窗口 | 当源代码管理处于非活动状态时，源代码管理 VSPackage 将隐藏它拥有的任何工具窗口。 |
| 特定于源代码管理 VSPackage 的选项页 | 注册表 **项 HKLM\SOFTWARE\Microsoft\VisualStudio\X.Y\ToolsOptionsPages\VisibilityCmdUIContexts** 允许 VSPackage 设置需要显示其选项页的上下文。 必须使用此项下的注册表项，使用源代码管理服务的 SID (ID) 并为其分配 DWORD 值 1。 每当在注册了源代码管理 VSPackage 的上下文中发生 UI 事件时，如果 VSPackage 处于活动状态，将调用 VSPackage。 |

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>
- <xref:EnvDTE.Constants.vsContextNoSolution>
- [管理 VSPackage](../../extensibility/managing-vspackages.md)
