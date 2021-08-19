---
title: Project模型核心组件|Microsoft Docs
description: 本文包含项目模型核心中标识的接口和服务的说明，以及与 对象关联的接口和服务。
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
ms.openlocfilehash: 8a0993a35a9de27ddbfe03ae25e47cdb74af2429
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122063000"
---
# <a name="project-model-core-components"></a>项目模型核心组件
下表扩展了项目模型。 这些表简要描述了模型中标识的接口和服务，以及与特定对象关联的接口和服务。 此外，这些表还详细说明了项目创建和维护中可选的其他接口，具体取决于特定项目类型的要求。

 有关详细信息，请参阅支持 [Symbol-Browsing 工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)。

### <a name="package-object"></a>包对象

|接口|注释|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>|在 IDE 中初始化 VSPackage，使其服务可用于 IDE。|

### <a name="project-factory-object"></a>Project工厂对象

|接口|注释|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|管理创建新项目和打开现有项目。|

### <a name="project-objects"></a>Project对象

|界面|注释|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>|管理项目项的添加和删除，打开编辑器，并维护每个文档名字对象和 之间的映射 `VSITEMID` 。 继承自 `IVsProject` 和 `IVsProject2` 。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|管理导航和显示属性并提供事件。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>|为仅在焦点位于焦点下的命令（如剪切和重命名）启用类似于 `IOleCommandTarget` 的命令执行解决方案资源管理器。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|用作项目层次结构的主命令目标接口。 它是用于查询对象的命令状态或状态以及正在运行的命令的标准接口。 当不在"焦点"窗口中时Project可用。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|协调项目状态持久性。 通常，项目状态存储为项目文件，但可以适应不基于文件的存储系统。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>|使项目能够管理其项目项的持久性的所有方面，可以是磁盘上的文件或其他存储系统中的对象。 `IVsPersistHierarchyItem2`接口用于未实现 接口的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> 项。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|协调与源代码控件的交互。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfgProvider>|使项目能够管理配置信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>|管理项目配置对象，例如调试/发布配置。 生成、部署和调试操作通过项目配置对象进行协调。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler>|由层次结构实现，用于控制删除 (破坏性) 或删除 (层次结构) 非破坏性对象选项。 从 接口调用 `IVsHierarchyDeleteHandler` 接口上的查询 `IVsHierarchy` 接口。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsGetCfgProvider>|提供实现选项，使 支持 接口的对象位于与实现 接口的项目对象不同的 `IVsCfgProvider2` COM `IVsHierarchy` 标识上。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectStartupServices>|实现可选接口，使项目由其他开发人员扩展。 该接口使第三方 VSPackage 能够注册你持久化到项目文件的 GUID，以便每次加载项目时，都会将第三方服务 GUID 加载到项目文件中并调用该 `IVsProjectStartupServices` `QueryService` GUID。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelperEvents>|由窗口中的源层次结构 `UIHierarchy` 实现，以协调剪贴板操作，例如剪切、复制和粘贴。 使用 `AdviseClipboardHelperEvents` 接口注册剪贴板事件。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataSource2>|提供有关 UI 层次结构窗口中拖放操作期间相对于其数据源的拖动项的信息。 从 接口 `IVsHierarchy` 调用。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataTarget>|提供有关 UI 层次结构窗口中拖放操作期间相对于其拖放目标的拖动项的信息。 从 接口 `IVsHierarchy` 调用。|

### <a name="configuration-object"></a>配置对象

|界面|注释|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>|提供有关配置的信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>|使项目能够管理配置信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|使项目能够在调试器控制下运行。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>|由为其他项目执行部署操作部署项目的部署项目实现。|

### <a name="configuration-builder-object"></a>Configuration Builder 对象

|界面|注释|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>|管理项目配置的生成操作。|

### <a name="additional-project-objects"></a>其他Project对象

|界面|注释|
|----------------|--------------|
|`IDispatch`<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages>|在"属性"窗口中 **显示项** 属性。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs>|显示部署的输出。|

 下表提供了项目模型中标识的服务的简要说明。

### <a name="services"></a>服务

|服务|注释|
|-------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes>|由实现项目类型的 VSPackage 使用，以注册其项目工厂是否存在于 IDE 中。 调用 方法时，VSPackage 必须为此服务调用 `QueryService` 并注册 `IVsPackage::SetSite` 其项目工厂。 如果未 `SetSite` 调用 方法，则项目不会实例化。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|提供对 IDE 内部、当前解决方案的内置概念的访问，例如枚举项目、创建新项目、通知项目更改等。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>|由希望参与源代码管理的项目调用。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>|维护一个打开的文档表，以确定是否已打开一个或多个项目项。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument>|包含调用以使用标准编辑器或特定编辑器实际打开项目项的接口和方法。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>|所有项目在添加、删除或重命名其项时必须调用。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx>|管理对文件或目录的更改，在磁盘上更改所选文件时通知客户端。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>|所有项目和编辑器在脏项或保存它们之前必须调用它们。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager>|管理项目配置的生成和部署操作顺序。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger>|提供对用于大多数调试控件的低级别调试器服务的访问。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>|允许 VSPackage 访问有关当前选择的信息，并启用与"属性 **"窗口** 的通信。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|提供与 UI 相关的基本 IDE 功能，例如创建和枚举工具窗口或文档窗口或向用户报告错误的功能。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>|提供对 IDE 状态栏的访问。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibility3>|用于实现自动化模型。 在项目模型中，将返回一个属性对象，该对象可用于创建该对象的实例。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper>|用于在层次结构中的项目对象上实现剪贴板事件。 `SVsUIHierWinClipboardHelper` 使你能够正确处理剪切、复制和粘贴操作。|

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [不在生成中：使用 HierUtil7 Project 类实现 Project 类型 (C++) ](/previous-versions/bb166212(v=vs.100))
- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)