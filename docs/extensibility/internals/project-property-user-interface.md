---
title: 项目属性用户界面 |Microsoft Docs
description: 了解项目子类型如何修改基项目提供的"属性页"对话框。
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
ms.workload:
- vssdk
ms.openlocfilehash: 77e3554f2a3fd3b0dc1d608bb7d0a1198116a4e3
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903584"
---
# <a name="project-property-user-interface"></a>项目属性用户界面

项目子类型可以使用项目"属性页"对话框中由基本项目提供的项，隐藏或创建只读控件和整个页面（如提供）或将项目子类型特定的页添加到"属性页"对话框。 

## <a name="extending-the-project-property-dialog-box"></a>扩展"项目属性"对话框

项目子类型实现自动化扩展程序以及项目配置浏览对象。 这些扩展程序实现 <xref:EnvDTE.IFilterProperties> 接口，使特定属性隐藏或只读。 基 **项目的** "属性页"对话框（由基础项目实现）将执行自动化扩展程序执行的筛选。

下面概述了扩展 **"项目属性** "对话框的过程：

- 基项目通过实现 接口从项目子类型检索扩展 <xref:EnvDTE80.IInternalExtenderProvider> 程序。 基本项目的浏览、项目自动化和项目配置浏览对象都实现此接口。

- 项目的实现浏览对象和项目自动化对象委托到项目子类型聚合器实现，即 (针对项目对象聚合器 <xref:EnvDTE80.IInternalExtenderProvider> <xref:EnvDTE80.IInternalExtenderProvider> `QueryInterface` <xref:EnvDTE80.IInternalExtenderProvider> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>) 。

- 基本项目配置浏览对象还实现 ，以从项目子类型配置对象直接在 <xref:EnvDTE80.IInternalExtenderProvider> 自动化扩展程序中连接。 其实现委托给 <xref:EnvDTE80.IInternalExtenderProvider> 由项目子类型聚合器实现的接口。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetProjectItem%2A>由项目配置浏览对象实现，返回 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 对象。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetCfg%2A>（也由项目配置浏览对象实现）返回 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg> 对象。

- 项目子类型可以通过检索以下值，确定基项目的各种可扩展对象的适当 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> CATID：

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_ExtObjectCATID>

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_BrowseObjectCATID>

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_CfgBrowseObjectCATID>

若要确定项目范围的 CATID，项目子类型将检索 [VSITEMID 的上述属性。中的](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>) 根 `VSITEMID typedef` 。 项目子类型可能还希望 **控制为项目** 显示的属性页对话框页，这些页面与配置无关。 某些项目子类型可能需要删除内置页面并添加特定于项目子类型的页面。 为了启用此功能，托管客户端项目为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> 以下属性调用 方法：

- `VSHPROPID_PropertyPagesCLSIDList` - 以分号分隔的独立于配置的属性页的 CLSID 列表。

- `VSHPROPID_CfgPropertyPagesCLSIDList —` 由分号分隔的依赖于配置的属性页的 CLSID 列表。

由于项目子类型聚合对象，因此它可以重写这些属性的定义， <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 以控制显示 **哪些属性页** 对话框。 项目子类型可以从内部基项目中检索这些属性，然后根据需要添加或删除 CLSID。

项目子类型添加的新属性页从基本项目实现中为项目配置浏览对象提供。 此项目配置浏览对象支持自动化扩展程序。 有关 AutomationExtenders 详细信息，请参阅 [Implementing and Using Automation Extenders](/previous-versions/0y92k2w2(v=vs.140))。 由项目子类型实现的属性页调用以检索其自己的项目子类型配置浏览对象，该对象扩展了基本项目的配置 <xref:EnvDTE.Project.Extender%2A> 浏览对象。

## <a name="see-also"></a>另请参阅

- <xref:EnvDTE.IFilterProperties>
- ["属性页"对话框](/previous-versions/visualstudio/visual-studio-2010/as5chysf(v=vs.100))