---
title: 可用服务列表|Microsoft Docs
description: 查看 Visual Studio 和 Visual Studio SDK 支持的可用服务的列表，包括用于获取每个服务的接口的服务 GUID。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- services, Visual Studio
- Visual Studio, services
ms.assetid: 724eb24b-b87c-4971-a2e7-adee7afc03b2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 06bb1c6c7b5e41f3c948abbbd633ba5e516a640c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110509"
---
# <a name="list-of-available-services"></a>可用服务的列表

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]和 Visual Studio SDK 支持以下服务。 某些包提供此处未列出的自己的服务，例如，语言服务没有单个服务 GUID。 必须使用语言的名称在注册表中查找语言服务的 GUID。

使用此处列出的服务 GUID 或者从其他一些源 (例如，语言服务) 获取每个服务显示的主接口。

## <a name="the-services"></a>服务

| 服务 | 接口 | Visual Studio | Visual Studio 2005 | 说明 |
| - | - |---------------|--------------------| - |
| <xref:Microsoft.VisualStudio.OLE.Interop.SBindHost> | <xref:Microsoft.VisualStudio.OLE.Interop.IBindHost> | 是 | 是 | 由 VSPackage 用于从 ActiveX 控件获取接口 <xref:Microsoft.VisualStudio.OLE.Interop.IBindHost> ，以简化异步数据传输。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SDTE> | <xref:EnvDTE.DTE> | 否 | 是 | 获取用于自动化的 DTE (设计) 扩展性。<br /><br /> C/C++ ID：SID_SDTE |
| <xref:Microsoft.VisualStudio.Shell.Interop.SCodeNavigate> | <xref:Microsoft.VisualStudio.Shell.Interop.ICodeNavigate> | 是 | 是 | 由窗体设计器实现以显示 控件的默认事件处理程序。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SContainerDispatch> | IDispatch | 是 | 是 | 使 VSPackage 能够访问另一个 VSPackage 或控件的自动化接口。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SExtendedTypeLib> | <xref:Microsoft.VisualStudio.Shell.Interop.IExtendedTypeLib> | 是 | 是 | 使 VSPackage 能够添加或创建扩展类型库。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SDirList> | <xref:Microsoft.VisualStudio.Shell.Interop.IDirList> | 否 | 是 | 提供对容器的命名列表的访问;例如，要搜索的目录列表，如"查找和替换"下拉列表中的"查找和替换"对话框中所示。 <xref:Microsoft.VisualStudio.Shell.Interop.IDirList>可以从 中读取对象，也可以写入对象。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SIVsPackageDynamicToolOwner> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwner> | 是 | 是 | 使 VSPackage 能够动态显示或隐藏自己的工具窗口。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SLicensedClassManager> | <xref:Microsoft.VisualStudio.Shell.Interop.ILicensedClassManager> | 是 | 是 | 通过指定许可证密钥列表，使 VSPackage 能够向其所需的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 类指示。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry> | <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> | 是 | 是 | 使 VSPackage 能够访问相对于本地注册表配置单元 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的注册表。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SOleComponentManager> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleComponentManager> | 是 | 是 | 提供组件协调服务，例如消息循环、键盘循环和事件通知。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager> | 是 | 是 | 使 VSPackage 能够访问各种用户界面 (UI) 元素（如帮助、状态栏和 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] UI 事件）。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponent> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> | 是 | 是 | 使 VSPackage 能够将其 UI 与 的 UI 集成 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponentSite> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentSite> | 是 | 是 | 使 VSPackage 能够控制特定于工具的 UI 更改。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SOleUndoManager> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> | 是 | 是 | 使 VSPackage 能够访问容器的撤消管理器，以参与该容器的撤消堆栈或访问该容器的撤消堆栈。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SProfferService> | <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> | 是 | 是 | 使 VSPackage 能够提供其自己的服务。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SProfferTypeLib> | <xref:Microsoft.VisualStudio.Shell.Interop.IProfferTypeLib> | 是 | 是 | 使窗体设计器能够使类型库可供引用。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> | <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> | 是 | 是 | 提供对选择容器中的选择的访问。 由窗体设计器使用。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SUIHostCommandDispatcher> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> | 是 | 是 | 使 VSPackage 能够参与命令处理程序链，并代表集成开发环境或 IDE (处理) 命令。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SUIHostLocale> | <xref:Microsoft.VisualStudio.Shell.Interop.IUIHostLocale> | 是 | 是 | 提供对主机的 UI 区域设置信息的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> | 否 | 是 | 启用 VSPackage，以在启用日志记录时记录高级消息。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddProjectItemDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddProjectItemDlg> | 是 | 是 | 提供对"添加Project **项**"对话框的访问权限，允许 VSPackage 实现自己的"添加 **项"** 菜单选项。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddWebReferenceDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg> | 是 | 是 | 显示" **添加引用"** 对话框。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine> | 是 | 是 | 使 VSPackage 能够确定是否为命令行开关devenv.exe。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCallBrowser> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCallBrowser> | 否 | 是 | 使 VSPackage 能够 **创建一调用浏览器** 调试中使用的新脚本。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsClassView> | 是 | 是 | 使 VSPackage 能够将 **类视图同步到** 特定对象。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCmdNameMapping> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCmdNameMapping> | 是 | 是 | 支持将命令名称映射到 GUID 以及返回并确定所有可用命令和名称的名称。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeDefView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeDefView> | 否 | 是 | 使 VSPackage 能够操作 **代码定义视图**。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeShareHandler> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeShareHandler> | 是 | 是 | 内部服务。 请勿使用。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindow> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> | 是 | 是 | 提供对可包含一个或多个文档的代码窗口的访问。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindowManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> | 是 | 是 | 使 VSPackage 可以将更改添加到代码窗口，如下拉栏。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindow> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow2> | 是 | 是 | 启用 VSPackage 以通过 **命令窗口** 运行命令，否则与 **命令窗口** 交互。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindowsCollection> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindowsCollection> | 否 | 是 | 使 VSPackage 能够操作由维护的 **命令** 窗口的列表 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComplusLibrary> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLibraryReferenceManager> | 是 | 是 | 使 VSPackage 能够向 **对象浏览器** 提供浏览信息。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg> | 否 | 是 | 启用 VSPackage 以支持 " **添加引用** " 选项，该选项使用户可以选择要添加到项目中的外部组件。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg2> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg2> | 否 | 是 | 启用 VSPackage 以支持 " **添加引用** " 选项，该选项使用户可以选择要添加到项目中的外部组件。 此版本的对话框允许在显示组件列表前对其进行预先填充。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsConfigurationManagerDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsConfigurationManagerDlg> | 否 | 是 | 显示 " **Configuration Manager** " 对话框。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject> | 否 | 是 | 允许 VSPackage 创建一个包含其他项目集合的项目。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDebuggableProtocol> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProtocol> | 是 | 是 | 允许 VSPackage 更新 IDE 用于启动特定调试引擎的可调试协议的列表。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDebugLaunch> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugLaunch> | 是 | 是 | 启用 VSPackage 以支持启动调试器。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDiscoveryService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDiscoveryService> | 是 | 是 | 允许 VSPackage 创建用于发现 Web 服务的发现会话。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsEnumHierarchyItemsFactory> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory> | 是 | 是 | 提供一个工厂，用于创建 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory> 用于枚举指定层次结构 (项目) 的对象。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsErrorList> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsErrorList> | 否 | 是 | 提供用于操作 " **生成错误列表** 任务" 窗口的其他方法。 具体而言，将 **生成错误列表** 任务窗口引入到 forefront，并强制显示所有错误。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager> | 是 | 是 | 提供对当前解决方案的 **杂项文件** 项目节点的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChange> | | 是 | 是 | 已过时。 改为使用 `SVsFileChangeEx` 服务。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx> | 是 | 是 | 允许 VSPackage 获取对 IDE 触发的各种文件更改事件的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterAddProjectItemDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> | 是 | 是 | 启用 VSPackage 以筛选在 " **添加项** " 对话框中显示的项。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterKeys> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterKeys> | 是 | 是 | 允许 VSPackage 执行高级键盘筛选。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorCacheManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> | 否 | 是 | 提供对中的字体和颜色的一组缓存的访问， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 以便刷新或清除特定缓存或所有缓存。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorStorage> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorUtilities> | 是 | 是 | 使 VSPackage 能够操作由维护的字体和颜色设置 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 此外，此服务提供对用于操作字体和颜色数据的实用工具方法集合的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> | 是 | 是 | 提供 "常规 **输出窗口** " 窗格的访问权限，并根据需要创建该窗格。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsHelpService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsHelpSystem> | 是 | 是 | 提供对帮助系统的访问权限。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsHTMLConverter> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsHTMLConverter> | 是 | 是 | 由调试器用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 来处理 HTML，以设置其输出的格式。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIME> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIME> | 是 | 是 | 在 VSPackage 中提供对输入法编辑器 (IME) API 的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntegratedHelp> | <xref:Microsoft.VisualStudio.VSHelp.SVsHelp> | 是 | 是 | 提供对 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 帮助系统进行关键字或 URL 访问的访问，以及通过帮助文件的导航控件。 此服务仅在以下情况下可用：将帮助集成到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 中，而不是作为外部程序运行。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntelliMouseHandler> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntelliMouseHandler> | 是 | 是 | 允许 VSPackage 访问智能鼠标轮功能，如在单击鼠标轮时使用鼠标轮和处理滚动和平移位图。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseEngine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseEngine> | 否 | 是 | 启用项目层次结构节点以加载或卸载文件，作为对 IntelliSense 操作的支持的一部分。 加载和卸载触发器事件的过程会影响项目的 IntelliSense 工具提示中显示的内容。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectHost> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectHost> | 否 | 是 | 使项目层次结构节点能够提供有关 (的嵌套 IntelliSense 项目的信息，这些项目实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject> 可在 IntelliSense 工具提示中显示的接口) 。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectManager> | 否 | 是 | 使项目层次结构节点可以通知事件侦听器，例如引用或配置中的更改，这些更改可能会影响 IntelliSense 工具提示中显示的内容。 设计为与包含语言一起使用。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsInvisibleEditorManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> | 是 | 是 | 使 VSPackage 能够注册"不可见"编辑器，即提供完整编辑功能但用户不可见的编辑器。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsLanguageFilter> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> | 是 | 是 | 使 VSPackage 能够向文本视图提供附加信息，例如数据提示和单词范围。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPad> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad> | 是 | 是 | 使 VSPackage 能够执行临时批处理脚本、执行输出发送到输出窗格的命令行程序，以及分析发送到错误窗口的标准警告和错误消息。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPadFactory> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPadFactory> | 是 | 是 | 提供用于创建 对象的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad> 工厂。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsLinkedUndoTransactionManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager> | 是 | 是 | 提供对链接的撤消管理器的访问权限。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsMenuEditor> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditorFactory> | 是 | 是 | 使窗体设计器能够访问共享菜单编辑器。 可以针对 查询 IVsMenuEditorFactory。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditor> |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsMonitorUserContext> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext> | 是 | 是 | 使 VSPackage 能够创建"上下文包"，该包用于关联特定上下文的帮助关键字。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjBrowser> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjBrowser> | 是 | 是 | 使 VSPackage 能够导航到对象浏览器 **中的特定对象**。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager> | 是 | 是 | 使 VSPackage 能够将其库管理器注册到 ，以管理命名空间、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 类和枚举等对象。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectSearch> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectSearch> | 是 | 是 | 使 VSPackage 能够搜索特定对象。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsOpenProjectOrSolutionDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOpenProjectOrSolutionDlg> | 否 | 是 | 使 VSPackage 能够使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 标准对话框打开项目或解决方案。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> | 是 | 是 | 使 VSPackage 能够在常规"输出"窗口中创建其他输出窗格。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsParseCommandLine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsParseCommandLine> | 是 | 是 | 使 接口的实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 者能够分析命令行。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPathVariableResolver> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPathVariableResolver> | 否 | 是 | 提供一种解析特定于 和 的变量的方法，这些变量 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 嵌入到路径中以生成最终路径。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPreviewChangesService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPreviewChangesService> | 否 | 是 | 显示 **用于** 重构代码的"预览更改"对话框。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsProfileDataManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsProfileDataManager> | 否 | 是 | 提供对配置文件管理器的访问权限，该管理器允许导入和导出设置数据，以及显示当前用户配置文件设置的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] UI。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsProfilesManagerUI> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsProfilesManagerUI> | 否 | 是 | 显示一个对话框，其中显示当前用户的配置文件设置。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPropertyPageFrame> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPageFrame> | 是 | 是 | 使 VSPackage 可以替代最初显示在"属性"窗口中 **的属性** 页。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> | 否 | 是 | 由 VSPackage 用于通知源代码管理提供程序文件即将在内存中更改或保存。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterDebugTargetProvider> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectDebugTargetProvider> | 否 | 是 | 使 VSPackage 项目能够以编程方式重写目标以在调试器中启动。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterEditors> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors> | 是 | 是 | 使 VSPackage 能够向 IDE 注册编辑器工厂。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsRegisterFindScope> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsRegisterFindScope> | 否 | 是 | 使 VSPackage 能够注册"在文件中查找 **"对话框的** 搜索范围。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterPriorityCommandTarget> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget> | 是 | 是 | 使 VSPackage 能够将自身注册为高优先级命令处理程序，使 VSPackage 能够查看所有命令。 请谨慎使用 （如果）。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes> | 是 | 是 | 使 VSPackage 能够向 IDE 注册项目类型。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceManager> | 否 | 是 | 使 VSPackage 能够从附属 DLL 加载托管资源以及非托管资源。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceView> | 是 | 是 | 请 <xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView> 改为使用服务。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> | 是 | 是 | 提供对跟踪所有当前打开的文档的 IDE (RDT) 的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> | 否 | 是 | 使 VSPackage 能够向源代码管理提供程序注册自身，以便它们可以参与源代码管理。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccToolsOptions> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions> | 是 | 是 | 启用 VSPackage，获取和设置源代码管理提供程序选项。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSettingsReader> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsReader> | 否 | 是 | 提供对用户配置文件设置的读取访问权限。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell> | 是 | 是 | 使 VSPackage 能够直接与其他 VSPackage 交互并对其进行操作。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger> | 是 | 是 | 提供对 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试器的访问权限。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> | 是 | 是 | 使 VSPackage 能够访问当前选择和管理命令 UI 上下文。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDCodeDomProvider> | IVSMDCodeDomProvider | 否 | 是 | 提供对 DOM 提供程序中的代码 (模型) ，可在本机代码中使用。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDDesignerService> | IVSMDCodeDomCreator<br /><br /> IVSMDDesignerService | 否 | 是 | 提供对托管窗体设计器的 IDE 支持的访问。 `IVSMDCodeDomCreator`可用于创建代码 DOM 提供程序。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDPropertyBrowser> | IVSMDPropertyBrowser | 否 | 是 | 提供对设计器属性窗口服务的访问权限。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDTypeResolutionService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVSMDTypeResolutionService> | 否 | 是 | 提供对接口的访问，该接口可返回 <xref:System.ComponentModel.Design.ITypeResolutionService> 可在本机代码中使用的对象。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSmartOpenScope> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSmartOpenScope> | 否 | 是 | 提供一种在程序集上打开作用域的方法，同时考虑根据需要锁定。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> | 是 | 是 | 提供对当前解决方案的顶级访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager> | 是 | 是 | 使 VSPackage 能够与解决方案的生成过程进行交互。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionObject> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> | 是 | 是 | 请 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> 改为使用 服务。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionPersistence> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> | 是 | 是 | 使 VSPackage 能够存储和检索当前解决方案的 .sln 文件中的信息。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSQLCLRReferences> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSQLCLRReferences> | 否 | 是 | 提供在托管代码程序集中添加和更新引用的能力。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStartPageDownload> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStartPageDownload> | 否 | 是 | 提供对 Visual Studio 2017 起始页下载服务的访问权限，以在后台线程上启动和停止下载服务。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar> | 是 | 是 | 提供对 IDE 状态栏的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStrongNameKeys> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStrongNameKeys> | 否 | 是 | 提供对方法的访问权限，这些方法用于创建强密钥名称和密钥文件，这些密钥文件具有用于对托管代码程序集进行签名的密码。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStructuredFileIO> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStructuredFileIO> | 是 | 是 | 使 VSPackage 支持以多种格式保存数据。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> | 是 | 是 | 提供对 IDE 的"任务列表的访问。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextImageUtilities> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextImageUtilities> | 否 | 是 | 提供用于加载和保存文本文件的实用工具。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> | 是 | 是 | 提供对 IDE 中可用的隐藏区域的所有文本缓冲区 (隐藏) 会话的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTextOut> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTextOut> | 是 | 是 | 提供 Win32 函数的版本，用于将文本写入设备上下文 `TextOut` (需要 DC 句柄) 。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextSpanSet> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextSpanSet> | 是 | 是 | 提供对文本图像或缓冲区中文本范围列表的访问。 此服务通常在文档容器上实现，并引用当前文档。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadedWaitDialog> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadedWaitDialog> | 否 | 是 | 使 VSPackage 能够显示一个对话框，该对话框等待其他线程 (等待后台任务) 。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadPool> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadPool> | 否 | 是 | 使 VSPackage 能够启动随后由 维护的后台任务 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox> | 是 | 是 | 提供对 IDE 工具箱 **的访问**。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxActiveXDataProvider> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProvider> | 是 | 是 | 使 VSPackage 能够从工具箱 **项获取** 信息。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxDataProviderRegistry> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProviderRegistry> | 否 | 是 | 使 VSPackage 能够注册工具箱数据提供程序，而不会产生预加载整个工具箱 的性能 **成本**。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolsOptions> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolsOptions> | 否 | 是 | 使 VSPackage 能够 **确定是否打开"** 选项"对话框并刷新所有选项页的可见性。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3> | 否 | 是 | 使 VSPackage 能够监视项目文件中所做的更改，并提供对源代码管理提供程序的批处理控制。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> | 是 | 是 | 使 VSPackage 能够通知 IDE 对所选内容所做的更改，这些更改可能会影响当前选定的项目项。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelper> | 是 | 是 | 启用层次结构 (如项目 VSPackage) 以协调剪贴板与其他层次结构的使用。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> | 是 | 是 | 提供对 IDE 的 UI 元素（如工具窗口和文档窗口）的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellDocumentWindowMgr> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellDocumentWindowMgr> | 是 | 是 | 使 VSPackage 能够基于数据流的内容还原所有窗口的位置，或将所有窗口的位置保存到流中。 很少使用。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument> | 是 | 是 | 使 VSPackage 能够以多种方式打开文档并确定谁拥有哪个文档。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> | 否 | 是 | 由 接口的实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 者用来报告错误和信息性消息。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebBrowsingService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebBrowsingService> | 是 | 是 | 使 VSPackage 能够创建和控制Web 浏览会话。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebFavorites> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebFavorites> | 是 | 是 | 使 VSPackage 能够添加到用户的 **收藏夹列表。** |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebPreview> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebPreview> | 是 | 是 | 使 VSPackage 可以预览网页（通常在子窗口中）。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebURLMRU> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebURLMRU> | 是 | 是 | 使 VSPackage 能够将 URL 添加到 URL (MRU) 列表中，并获取 MRU 列表中所有 URL 的列表。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWindowFrame> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> | 是 | 是 | 使 VSPackage 能够获取包或包的一部分可能位于其中的窗口框架。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsXMLMemberIndexService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsXMLMemberIndexService> | 是 | 是 | 提供对与特定元数据文件关联的 XML 格式文档文件的访问权限。 |

## <a name="see-also"></a>请参阅

- [使用并提供服务](../../extensibility/using-and-providing-services.md)
