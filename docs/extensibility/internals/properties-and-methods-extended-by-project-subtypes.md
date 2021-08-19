---
title: 由子类型Project扩展的属性|Microsoft Docs
description: 了解项目子类型可以增强或修改的功能，通过这些功能可以自定义项目系统的行为Visual Studio。
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
ms.openlocfilehash: 0744b8669e3ab5d2fe7a3e936157172c5b0e0ef2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122117665"
---
# <a name="properties-and-methods-extended-by-project-subtypes"></a>项目子类型扩展的属性和方法
项目子类型具有影响项目行为的很大能力，因为它被构造为基本项目的聚合器。 本部分总结了项目子类型可以增强或修改的一些功能。

## <a name="features-gained-by-aggregation"></a>聚合获得的功能
 下表总结了聚合使项目子类型能够在基项目中重写的许多方法。

|聚合重写的方法|Project亚|
|---------------------------------------|---------------------|
|从 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>：<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetGuidProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetGuidProperty%2A>|使项目子类型能够<br /><br /> - 更改项目节点的标题和图标。<br />- 完全重写项目 `Browse` 对象。<br />- 控制是否可以重命名项目。<br />- 控制排序顺序。<br />- 控制动态帮助的用户上下文。|
|从 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>：<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetItemContext%2A>|使项目子类型能够控制向设计器和编辑器提供哪些上下文服务。|
|从 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>：<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A><br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>|使项目子类型能够<br /><br /> - 参与项目命令的命令路由。<br />- 添加、删除或禁用项目环境命令解决方案资源管理器活动命令。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>|使项目子类型能够筛选用户在"添加新项" **对话框中看到内容** 。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGeneratorFactory>|使项目子类型能够<br /><br /> - 确定给定文件扩展名的默认生成器。<br />- 将人工可读生成器名称映射到 COM 对象。|

## <a name="properties-used-by-project-subtypes"></a>子Project使用的属性
 环境和基本项目系统可以使用下表中详述的 和 枚举的属性，使项目子类型能够控制项目 <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID> <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> 系统的各种功能。

|VSHPROPID 属性|Project亚|
|------------------------|---------------------|
|`AddItemTemplatesGuid`|允许项目子类型控制"添加项 **"对话框** 的内容。 项目子类型可以提供模板目录的新规范、添加新类型的项、删除现有项，以及重新组织基本项目的"添加项"对话框中项 **的** 子集。|
|`PropertyPagesCLSIDList`|允许项目子类型添加或删除与配置无关的属性页。|
|`CfgPropertyPagesCLSIDList`|允许项目子类型添加或删除依赖于配置的属性页。|
|`ExtObjectCATID`|允许项目子类型通过了解扩展程序 CATID 为项目或项目项对象提供自动化扩展程序。 例如，项目子类型可以提供自定义 `Project.Extender("<subtype>")` 对象。|
|`BrowseObjectCATID`|允许项目子类型通过了解扩展程序 CATID 为 对象 `Browse` 提供自动化扩展程序。 例如，项目子类型可以将额外的属性添加到 <xref:EnvDTE.Project.Properties%2A> 集合中。|
|`CfgBrowseObjectCATID`|允许项目子类型为项目配置浏览对象提供自动化扩展程序。 例如，项目子类型可以将额外的属性添加到 <xref:EnvDTE.Configuration.Properties%2A> 集合中。|
|`CfgExtObjectCATID`|允许项目子类型为配置对象提供自动化扩展程序。|
|`DefaultPlatformName`|允许项目子类型确定项目配置对象的平台名称。|

 基本项目提供上述属性的默认实现。 基项目通过调用最外层项目子类型的 for 获取这些属性，从而允许项目 `QueryInterface` <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 子类型重写属性的实现。

## <a name="see-also"></a>请参阅
- [项目子类型设计](../../extensibility/internals/project-subtypes-design.md)
