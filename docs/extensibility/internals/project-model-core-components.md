---
title: Project模型核心组件 |Microsoft Docs
description: 本文包含在项目模型核心中标识的接口和服务的说明，以及与对象关联的接口和服务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project models, objects and interfaces
- project models, services
ms.assetid: b2f572d3-b26d-4846-92d1-84055fac141a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 9440fcd6201c629e8151002faea373ccf783263205dbee32589ea96ac7c7b322
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432262"
---
# <a name="project-model-core-components"></a>项目模型核心组件
下表在项目模型上展开。 这些表显示了模型中标识的接口和服务的简短说明，以及与特定对象关联的接口和服务。 此外，这些表详细说明了在创建和维护项目时可以选择的其他接口，具体取决于特定的项目类型的要求。

 有关详细信息，请参阅 [支持 Symbol-Browsing 工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)。

### <a name="package-object"></a>Package 对象

|接口|注释|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>|在 IDE 中初始化 VSPackage，并使其服务可供 IDE 使用。|

### <a name="project-factory-object"></a>Project工厂对象

|接口|注释|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|管理创建新项目和打开现有项目。|

### <a name="project-objects"></a>Project 对象

|接口|注释|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>|管理添加和删除项目项、打开编辑器，以及维护每个文档名字对象和之间的映射 `VSITEMID` 。 继承自 `IVsProject` 和 `IVsProject2` 。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|管理导航和显示属性并提供事件。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>|启用命令执行，类似于 `IOleCommandTarget` "剪切" 和 "重命名" 等命令的执行，仅当焦点在解决方案资源管理器时才适用。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|用作项目层次结构的主命令目标接口。 它是用于查询对象的命令状态或状态以及运行命令的标准接口。 当你未在 "Project" 窗口中重点时可用。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|协调项目状态的持久性。 通常情况下，项目状态存储为项目文件，但可改编为非基于文件的存储系统。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>|使项目可以管理其项目项的持久性的所有方面，可以是磁盘上的文件，也可以是其他存储系统中的对象。 `IVsPersistHierarchyItem2`接口用于未实现接口的项 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> 。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|与源代码管理协调交互。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfgProvider>|使项目能够管理配置信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>|管理项目配置对象，例如 "调试"/"发布" 配置。 生成、部署和调试操作通过项目配置对象进行协调。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler>|由层次结构实现，用于控制删除 (破坏性) 或删除 (层次结构项的非破坏性) 选项。 从接口调用接口上的查询接口 `IVsHierarchyDeleteHandler` `IVsHierarchy` 。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsGetCfgProvider>|提供实现选项，该选项使对象支持与 `IVsCfgProvider2` 实现该接口的项目对象不同的 COM 标识上的接口 `IVsHierarchy` 。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectStartupServices>|实现的可选接口，使你的项目可由其他开发人员进行扩展。 `IVsProjectStartupServices`接口允许第三方 VSPackage 注册一个保存在项目文件中的 GUID，以便每次加载项目时，会将第三方服务 GUID 加载到项目文件中，并调用 `QueryService` 该 guid。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelperEvents>|由窗口中的源层次结构实现 `UIHierarchy` ，用于协调剪贴板操作，例如剪切、复制和粘贴。 使用 `AdviseClipboardHelperEvents` 接口注册剪贴板事件。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataSource2>|在 UI 层次结构窗口中的拖放操作过程中，提供有关拖动项相对于其数据源的信息。 从接口调用 `IVsHierarchy` 。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataTarget>|在 UI 层次结构窗口中的拖放操作过程中，提供与拖放操作相关的拖动项的相关信息。 从接口调用 `IVsHierarchy` 。|

### <a name="configuration-object"></a>配置对象

|接口|注释|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>|提供有关配置的信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>|使项目能够管理配置信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|使项目可以在调试器的控制下运行。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>|由执行其他项目的部署操作的部署项目实现。|

### <a name="configuration-builder-object"></a>配置生成器对象

|接口|注释|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>|管理项目配置的生成操作。|

### <a name="additional-project-objects"></a>其他 Project 对象

|接口|注释|
|----------------|--------------|
|`IDispatch`<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages>|在 " **属性** " 窗口中显示项属性。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs>|显示部署的输出。|

 下表提供了在项目模型中标识的服务的简要说明。

### <a name="services"></a>服务

|服务|注释|
|-------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes>|由实现项目类型的 Vspackage 使用，用来注册 IDE 中是否存在其项目工厂。 `QueryService`调用方法时，VSPackage 必须调用此服务并注册其项目工厂 `IVsPackage::SetSite` 。 如果 `SetSite` 未调用方法，则不会实例化您的项目。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|提供对 IDE 的当前解决方案的内部内置概念的访问，例如，枚举项目、创建新项目、记录项目更改等功能。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>|由希望参与源代码管理的项目调用。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>|维护打开的文档的表，以确定是否有一个或多个项目项已打开。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument>|包含调用的接口和方法，以使用标准编辑器或特定编辑器实际打开项目项。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>|需要在添加、删除或重命名其项时由所有项目调用。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx>|管理对文件或目录的更改，并在磁盘上更改了选定文件时通知客户端。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>|需要在所有项目和编辑器进行脏项或保存之前调用。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager>|管理项目配置的生成和部署操作的顺序。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger>|提供对用于大多数调试控件的低级调试器服务的访问。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>|允许 Vspackage 访问有关当前所选内容的信息，并启用与 " **属性** " 窗口的通信。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|提供基本的 UI 相关 IDE 功能，如创建和枚举工具窗口或文档窗口的功能，或向用户报告错误。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>|提供对 IDE 状态栏的访问。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibility3>|用于实现自动化模型。 在您的项目模型中，您将返回一个 properties 对象，该对象可用于创建该对象的实例。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper>|用于在层次结构中的项目对象上实现剪贴板事件。 `SVsUIHierWinClipboardHelper` 允许您正确处理剪切、复制和粘贴操作。|

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [不在生成中：使用 HierUtil7 Project 类实现 Project 类型 (c + +) ](/previous-versions/bb166212(v=vs.100))
- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)