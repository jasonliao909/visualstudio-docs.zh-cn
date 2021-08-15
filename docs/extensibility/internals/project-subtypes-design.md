---
title: Project子类型设计|Microsoft Docs
description: 了解项目子类型如何允许 VSPackage 基于项目扩展Microsoft 生成引擎 (MSBuild) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project subtypes, design
ms.assetid: 405488bb-1362-40ed-b0f1-04a57fc98c56
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 0cea3cde98ab0f35d46be1169b5f47d538e1ff8294bb251a4e4b3d358b688b18
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432305"
---
# <a name="project-subtypes-design"></a>项目子类型设计

Project子类型允许 VSPackage 基于项目扩展Microsoft 生成引擎 (MSBuild) 。 使用聚合可以重复使用 中实现的大部分核心托管项目系统，但仍可以自定义特定 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 方案的行为。

 以下主题详细介绍项目子类型的基本设计和实现：

- Project子类型设计。

- 多级别聚合。

- 支持接口。

## <a name="project-subtype-design"></a>Project子类型设计

通过聚合 main 和 对象实现项目子类型的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> 初始化。 此聚合使项目子类型能够替代或增强基本项目大部分功能。 Project子类型第一次有机会使用 处理属性、使用 和 的命令以及 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 进行项目项管理 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> 。 Project子类型也可以扩展：

- Project配置对象。

- 依赖于配置的对象。

- 与配置无关的浏览对象。

- Project自动化对象。

- Project自动化属性集合。

有关按项目子类型扩展性的信息，请参阅属性和方法 扩展[Project子类型](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)。

### <a name="policy-files"></a>策略文件

环境提供了一个示例，说明在策略文件的实现中，使用项目子 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 类型扩展基本项目系统。 策略文件允许通过管理包括以下功能来调整环境：解决方案资源管理器、"添加Project"对话框、"添加新项"对话框和"属性 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] "对话框。    策略子类型通过 和 实现重写和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> `IOleCommandTarget` <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 增强这些功能。

### <a name="aggregation-mechanism"></a>聚合机制

环境的项目子类型聚合机制支持多个级别的聚合，从而允许通过进一步风格化项目实现高级子类型。 此外，项目子类型的支持对象（如 ）旨在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg> 允许多个级别的分层。 为了符合 COM 和 COM 聚合规则的约束，需要以协作方式对项目子类型和基项目进行编程，以使内部子类型或基项目能够正确参与委托方法调用和管理引用计数。 也就是说，必须编程要聚合的项目以支持聚合。

下图显示了多级别项目子类型聚合的图示表示形式。

![图：Visual Studio 多级项目风格](../../extensibility/internals/media/vs_multilevelprojectflavor.gif)

多级别项目子类型聚合由三个级别组成，即一个基项目，由项目子类型聚合，然后由高级项目子类型进一步聚合。 该图重点介绍作为项目子类型体系结构的一部分提供的一些 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持接口。

### <a name="deployment-mechanisms"></a>部署机制

由项目子类型增强的许多基本项目系统功能包括部署机制。 项目子类型通过实现配置接口（例如 (和) 调用 上的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> QueryInterface）来影响部署机制 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> 。 在项目子类型和高级项目子类型都添加不同配置实现的情况下，基础项目对高级项目 `QueryInterface` 子类型的 调用 `IUnknown` 。 如果内部项目子类型包含基础项目请求的配置实现，则高级项目子类型将委托给内部项目子类型提供的实现。 作为一种将状态从一个聚合级别持久化到另一个聚合级别的机制，项目子类型的所有级别都实现 ，以将非生成相关的 XML 数据 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 持久保存到项目文件中。 有关详细信息，请参阅在文件[文件中MSBuild Project数据](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)。 <xref:EnvDTE80.IInternalExtenderProvider> 作为从项目子类型检索自动化扩展程序的机制实现。

下图重点介绍自动化扩展程序实现，特别是项目子类型用来扩展基本项目系统的项目配置浏览对象。

![图：VS 项目风格自动扩展程序](../../extensibility/internals/media/vs_projectflavorautoextender.gif)

Project子类型可以通过扩展自动化对象模型来进一步扩展基本项目系统。 这些对象定义为 DTE 自动化对象的一部分，用于扩展Project对象、对象 `ProjectItem` 和 `Configuration` 对象。 有关详细信息，请参阅[扩展基类对象](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)Project。

## <a name="multi-level-aggregation"></a>多级别聚合

包装较低级别项目子类型的项目子类型实现需要以协作方式编程，以使内部项目子类型正常工作。 编程职责列表包括：

- 包装内部子类型的项目子类型的实现必须委托给 和 方法的内部项目 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 子类型的 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A> 实现。

- 包装 <xref:EnvDTE80.IInternalExtenderProvider> 项目子类型的实现必须委托给其内部项目子类型的实现。 具体而言， 的实现需要从内部项目子类型获取名称的字符串，然后连接要添加为 <xref:EnvDTE80.IInternalExtenderProvider.GetExtenderNames%2A> 扩展程序的字符串。

- 包装项目子类型的实现必须实例化其内部项目子类型的对象，并保留为私有委托，因为只有基项目的项目配置对象直接知道包装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg> 项目子类型配置对象存在。 外部项目子类型最初可以选择它想要直接处理的配置接口，然后将其余部分委托给内部项目子类型的 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg.get_CfgType%2A> 。

## <a name="supporting-interfaces"></a>支持接口

基本项目委托对项目子类型添加的支持接口的调用，以扩展其实现的各个方面。 这包括扩展项目配置对象和各种属性浏览器对象。 通过调用指向最 (子类型聚合) 的指针来检索这些 `QueryInterface` `punkOuter` `IUnknown` 接口。

|接口|Project亚|
|---------------|---------------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>|允许项目子类型：<br /><br /> - 提供 的实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> 。<br />- 通过允许项目子类型提供自己的 实现来控制调试器启动 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> 。<br />- 通过在其 的实现中适当处理大小写 `DBGLAUNCH_DesignTimeExprEval` 来禁用设计时表达式计算 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.QueryDebugLaunch%2A> 。|
|<xref:EnvDTE80.IInternalExtenderProvider>|允许项目子类型：<br /><br /> - 扩展 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject> 项目的 以添加或删除与配置无关的项目属性。<br />- 扩展项目自动化对象 () <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtObject> 项目的属性。<br /><br /> 上述属性值取自 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> 枚举。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>|允许项目子类型在给定项目 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg> 配置浏览对象时映射回对象。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBrowseObject>|给定项目配置浏览对象，允许项目子类型映射回 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> `VSITEMID` 或 对象。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>|允许项目子类型将任意 XML 结构化数据持久化到项目文件 (.vbproj 或 .csproj) 。 此数据对用户不可见MSBuild。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>|允许项目子类型：<br /><br /> - 添加新MSBuild属性。<br />- 从中删除不必要的MSBuild。<br />- 查询属性的当前MSBuild值。<br />- 更改属性的当前MSBuild值。|

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>
