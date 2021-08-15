---
title: Project配置对象|Microsoft Docs
description: 了解项目配置对象如何管理向 UI 显示配置信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project configurations, object
- objects, project configuration
ms.assetid: 877756c9-4261-43d9-9f32-51bf06b4219f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a84f6d8f635698ac02b05efac9fa3e3110d2e293f6e5ba5a3c7e3f96fe2a703c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121321267"
---
# <a name="project-configuration-object"></a>项目配置对象
项目配置对象管理向 UI 显示配置信息。

 ![Visual Studio Project配置](../../extensibility/internals/media/vsprojectcfg.gif "vsProjectCfg")Project配置属性页

 配置Project管理项目配置。 若要获取访问和检索有关项目配置的信息的环境和其他包，请调用附加到配置提供程序Project接口。

> [!NOTE]
> 无法以编程方式创建或编辑解决方案配置文件。 您必须使用 `DTE.SolutionBuilder`。 有关详细信息 [，请参阅](../../extensibility/internals/solution-configuration.md) 解决方案配置。

 若要发布在配置 UI 中使用的显示名称，项目应实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_DisplayName%2A> 。 环境调用 ，它返回可用于获取要列在环境 UI 中的配置和平台信息的显示名称的指针 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A> `IVsCfg` 列表。 活动配置和平台由活动解决方案配置中存储的项目配置确定。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager.FindActiveProjectCfg%2A>方法可用于检索活动项目配置。

 可以选择使用 对象在 对象上实现 对象，以便基于规范 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProviderEventsHelper> `IVsProjectCfg2` 项目配置名称检索对象。

 为环境和其他项目提供项目配置访问权限的另一种方式是让项目提供 方法的实现，以 `IVsCfgProvider2::GetCfgs` 返回一个或多个配置对象。 项目还可以实现 （继承自 ，因而继承自 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> `IVsProjectCfg` `IVsCfg` ）以提供特定于配置的信息。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> 支持平台以及用于添加、删除和重命名项目配置的功能。

> [!NOTE]
> 由于 Visual Studio 不再局限于两种配置类型，因此，处理配置的代码不应使用配置数量的假设编写，也不应在编写时假定只有一个配置的项目一定是 Debug 或 Retail。 这会使用 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsReleaseOnly%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsDebugOnly%2A> 已过时。

 对 `QueryInterface` 从 返回的对象调用 将 `IVsGetCfgProvider::GetCfgProvider` 检索 `IVsCfgProvider2` 。 如果在项目对象上调用 未找到 ，则可以通过对为 返回的对象调用层次结构根浏览器对象，或者通过指向为 返回的配置提供程序的指针来访问 `IVsGetCfgProvider` `QueryInterface` `IVsProject3` `QueryInterface` `IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_BrowseObject)` 配置提供程序对象 `IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_ConfigurationProvider)` 。

 `IVsProjectCfg2` 主要提供对生成、调试和部署管理对象的访问，并允许项目自由对输出进行分组。 和 的方法可用于实现 来管理生成过程，以及配置 `IVsProjectCfg` `IVsProjectCfg2` <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> 的输出组的指针。

 项目必须针对它支持的每个配置返回相同的组数，即使组中包含的输出数可能因配置而异。 这些组还必须具有相同的标识符信息 (规范名称、显示名称和组信息) 从配置到项目中的配置。 有关详细信息，请参阅输出[Project配置](../../extensibility/internals/project-configuration-for-output.md)。

 若要启用调试，配置应实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> 。 `IVsDebuggableProjectCfg` 是一个可选接口，由项目实现，以允许调试器启动配置，并且使用 和 在配置对象 `IVsCfg` 上实现 `IVsProjectCfg` 。 当用户选择按 F5 启动调试器时，环境会调用它。

 `ISpecifyPropertyPages``IDispatch`和 与属性页结合使用，以检索和显示与配置相关的信息。 有关详细信息，请参阅属性 [页](../../extensibility/internals/property-pages.md)。

## <a name="see-also"></a>另请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)
- [属性页](../../extensibility/internals/property-pages.md)
- [解决方案配置](../../extensibility/internals/solution-configuration.md)
