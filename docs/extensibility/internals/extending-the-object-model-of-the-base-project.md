---
title: 扩展基对象对象Project |Microsoft Docs
description: 了解如何使用项目子类型在 Visual Studio扩展基本项目的自动化对象模型。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: reference
helpviewer_keywords:
- automation object model, extending
- project subtypes, extending automation object model
- automation object model
ms.assetid: 2f95cc53-dff6-476c-bacd-500fb0ff7725
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 20f241515e70f161792279a98bac61bb8801377e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600732"
---
# <a name="extend-the-object-model-of-the-base-project"></a>扩展基础项目的对象模型

项目子类型可以扩展基项目的自动化对象模型，位置如下：

- Project。扩展 (" \<ProjectSubtypeName> ") ：这允许项目子类型提供对象，该对象具有 对象的自定义 <xref:EnvDTE.Project> 方法。 项目子类型可以使用自动化扩展程序来公开 `Project` 对象。 在主项目子类型聚合器上实现的接口应为 来自 的 提供其对象 (<xref:EnvDTE80.IInternalExtenderProvider> `VSHPROPID_ExtObjectCATID` 与 <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> `itemid` [VSITEMID 的值相对应。CATID](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) 根目录。

- ProjectItem.Extender (") ：这允许项目子类型为对象提供来自项目中特定 \<ProjectSubtypeName> 对象的 <xref:EnvDTE.ProjectItem> 自定义方法。 项目子类型可以使用自动化扩展程序来公开此对象。 在主项目子类型聚合器上实现的接口需要为 来自 的 提供其对象 (对应于所需的) <xref:EnvDTE80.IInternalExtenderProvider> `VSHPROPID_ExtObjectCATID` <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> <xref:Microsoft.VisualStudio.VSConstants.VSITEMID> CATID。

- Project。属性：此集合公开对象的与配置无关的 `Project` 属性。 有关 `Project` 属性的详细信息，请参阅 <xref:EnvDTE.Project.Properties%2A>。 项目子类型可以使用自动化扩展程序将其属性添加到此集合。 在主项目子类型聚合器上实现的接口需要为 来自 的 提供其对象 (<xref:EnvDTE80.IInternalExtenderProvider> `VSHPROPID_BrowseObjectCATID` 与 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> `itemid` [VSITEMID 的值相对应。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) CATID。

- Configuration.Properties：此集合公开特定配置项目的配置依赖属性，例如 (调试) 。 有关详细信息，请参阅 <xref:EnvDTE.Configuration>。 项目子类型可以使用自动化扩展程序将其属性添加到此集合。 在主项目子类型聚合器上实现的接口为 <xref:EnvDTE80.IInternalExtenderProvider> 对应于 `VSHPROPID_CfgBrowseObjectCATID` VSITEMID 值的 CATID (`itemid` [提供其 对象。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) 。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>接口用于区分一个配置浏览对象和另一个配置浏览对象。

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>
