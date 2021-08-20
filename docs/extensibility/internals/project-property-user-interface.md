---
title: Project属性用户界面 |Microsoft Docs
description: 了解项目子类型如何按基本项目的提供方式修改 "项目属性页" 对话框。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: reference
helpviewer_keywords:
- project properties [Visual Studio], user interface
- projects [Visual Studio SDK], properties UI
- project properties UI
ms.assetid: b6aec634-8533-476c-9ebd-36536a2288e2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6b1a854488be852c23fcfcc3287fc8a35c5adb6e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122094602"
---
# <a name="project-property-user-interface"></a>项目属性用户界面

项目子类型可以使用 "项目 **属性页** " 对话框中的项，因为它们由基本项目提供、隐藏或使只读控件和整页提供，或将特定于项目子类型的页添加到 " **属性页** " 对话框。

## <a name="extending-the-project-property-dialog-box"></a>扩展 "Project 属性" 对话框

项目子类型实现自动化扩展程序和项目配置浏览对象。 这些扩展程序实现了 <xref:EnvDTE.IFilterProperties> 接口，以使特定属性处于隐藏或只读状态。 基本项目实现的基本项目的 " **属性页** " 对话框将遵循自动化扩展程序执行的筛选。

下面概述了扩展 **Project 属性** 对话框的过程：

- 基项目通过实现接口，从项目子类型中检索扩展程序 <xref:EnvDTE80.IInternalExtenderProvider> 。 基本项目的 "浏览"、"项目自动化" 和 "项目配置" 浏览对象均实现此接口。

- 项目的 " <xref:EnvDTE80.IInternalExtenderProvider> 浏览对象" 和 "项目自动化" 对象委托的实现将委托给 <xref:EnvDTE80.IInternalExtenderProvider> 项目子类型聚合器的实现 (即，它们 `QueryInterface` <xref:EnvDTE80.IInternalExtenderProvider> 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 项目对象) 上。

- 基本项目配置 "浏览" 对象还实现了 <xref:EnvDTE80.IInternalExtenderProvider> 从 "项目子类型" 配置对象直接连接到自动化扩展器。 其实现委托给 <xref:EnvDTE80.IInternalExtenderProvider> 由项目子类型聚合器实现的接口。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetProjectItem%2A>由 "项目配置" 浏览对象实现，返回 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 对象。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetCfg%2A>还由项目配置浏览对象实现，它返回 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg> 对象。

- 项目子类型可以通过检索以下值在运行时为基本项目的各种可扩展对象确定相应的 Catid <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> ：

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_ExtObjectCATID>

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_BrowseObjectCATID>

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_CfgBrowseObjectCATID>

若要确定项目范围的 Catid，项目子类型将检索 VSITEMID 的上述属性 [。](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>) 中的根 `VSITEMID typedef` 。 项目子类型还可能需要控制为项目显示的 " **属性页** " 对话框页，分别为配置依赖项和独立配置。 某些项目子类型可能需要删除内置页面并添加特定于项目子类型的页面。 为实现此目的，托管客户端项目对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> 以下属性调用方法：

- `VSHPROPID_PropertyPagesCLSIDList` -以分号分隔的、独立于配置的属性页的 Clsid 列表。

- `VSHPROPID_CfgPropertyPagesCLSIDList —` 依赖于配置的属性页的 Clsid 列表（以分号分隔）。

由于项目子类型聚合 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 对象，因此它可以重写这些属性的定义以控制显示哪些 **属性页** 对话框。 项目子类型可以从内部基础项目中检索这些属性，并根据需要添加或删除 Clsid。

项目子类型添加的新属性页将从基本项目实现中传递项目配置浏览对象。 此项目配置浏览对象支持自动化扩展程序。 有关 AutomationExtenders 的详细信息，请参阅 [实现和使用自动化扩展](/previous-versions/0y92k2w2(v=vs.140))程序。 由项目子类型调用实现的属性页 <xref:EnvDTE.Project.Extender%2A> 检索其自己的项目子类型配置浏览对象，该对象扩展了基项目的配置浏览对象。

## <a name="see-also"></a>请参阅

- <xref:EnvDTE.IFilterProperties>
- ["属性页" 对话框](/previous-versions/visualstudio/visual-studio-2010/as5chysf(v=vs.100))