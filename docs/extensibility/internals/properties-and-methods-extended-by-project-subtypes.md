---
title: Project 子类型扩展的属性和方法 |Microsoft Docs
description: 了解项目子类型可以增强或修改的功能，这使你可以自定义 Visual Studio 的项目系统的行为。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project subtypes, extended methods
- project subtypes, extended properties
ms.assetid: 2b9833bf-8551-4ae1-93db-197ba645c65e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: d0fe9ed20b315afcae360e2535eec60a518a9604902cf494b9baf006a77aae72
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401292"
---
# <a name="properties-and-methods-extended-by-project-subtypes"></a>项目子类型扩展的属性和方法
项目子类型有很大的影响，因为它被构造为基本项目的聚合器。 本部分总结了项目子类型可以增强或修改的一些功能。

## <a name="features-gained-by-aggregation"></a>聚合获取的功能
 下表汇总了许多聚合使项目子类型在基本项目中重写的方法。

|聚合重写的方法|Project类型|
|---------------------------------------|---------------------|
|从 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>：<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetGuidProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetGuidProperty%2A>|使项目子类型成为<br /><br /> -更改项目节点的标题和图标。<br />-完全重写项目 `Browse` 对象。<br />-控制是否可以重命名项目。<br />-控制排序顺序。<br />-控制动态帮助的用户上下文。|
|从 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>：<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetItemContext%2A>|启用项目子类型，以控制向设计器和编辑器提供的上下文服务。|
|从 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>：<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A><br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>|使项目子类型成为<br /><br /> -参与项目命令的命令路由。<br />-添加、删除或禁用项目环境命令，并解决方案资源管理器活动命令。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>|启用项目子类型，以筛选用户在 " **添加新项** " 对话框中看到的内容。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGeneratorFactory>|使项目子类型成为<br /><br /> -确定给定文件扩展名的默认生成器。<br />-将可读的生成器名称映射到 COM 对象。|

## <a name="properties-used-by-project-subtypes"></a>Project 子类型使用的属性
 环境和基本项目系统可以使用 <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID> <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> 下表中详细说明的属性和枚举来启用项目子类型，以控制项目系统的各种功能。

|VSHPROPID 属性|Project类型|
|------------------------|---------------------|
|`AddItemTemplatesGuid`|允许项目子类型控制 " **添加项** " 对话框的内容。 项目子类型可以提供新的模板目录规范、添加新类型的项、删除现有项以及重新组织基本项目的 " **添加项** " 对话框中的项的子集。|
|`PropertyPagesCLSIDList`|允许项目子类型添加或删除独立于配置的属性页。|
|`CfgPropertyPagesCLSIDList`|允许项目子类型添加或删除依赖于配置的属性页。|
|`ExtObjectCATID`|通过了解扩展程序 CATID，允许项目子类型为项目或项目项对象提供自动化扩展程序。 例如，项目子类型可以提供自定义 `Project.Extender("<subtype>")` 对象。|
|`BrowseObjectCATID`|允许项目子类型 `Browse` 通过了解扩展程序 CATID 为对象提供自动化扩展器。 例如，项目子类型可以将额外的属性添加到 <xref:EnvDTE.Project.Properties%2A> 集合中。|
|`CfgBrowseObjectCATID`|允许项目子类型为项目配置浏览对象提供自动化扩展程序。 例如，项目子类型可以将额外的属性添加到 <xref:EnvDTE.Configuration.Properties%2A> 集合中。|
|`CfgExtObjectCATID`|允许项目子类型为配置对象提供自动化扩展程序。|
|`DefaultPlatformName`|允许项目子类型确定项目的配置对象的平台名称。|

 基本项目提供上述属性的默认实现。 基项目通过对 `QueryInterface` <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 最外面的项目子类型调用来获取这些属性，从而允许项目子类型重写属性的实现。

## <a name="see-also"></a>请参阅
- [项目子类型设计](../../extensibility/internals/project-subtypes-design.md)
