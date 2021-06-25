---
title: IDE 常量|Microsoft Docs
description: VSConstants 类提供特定于 IDE 且以前仅在头文件中定义的常量。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: reference
helpviewer_keywords:
- IDE, errors
- logical views
- errors [Visual Studio], IDE
- UI context constants
- constants, Visual Studio IDE
- IDE, constants
- physical views
ms.assetid: 5030e70a-241d-474a-ba8c-e3b1cf947ff0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 802de0fd29d909320040667f972de422595bdd4f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904963"
---
# <a name="ide-constants"></a>IDE 常量

<xref:Microsoft.VisualStudio.VSConstants>类提供特定于集成开发环境的常量 (IDE) 且以前仅在头文件中定义。

## <a name="logical-and-physical-views"></a>逻辑视图和物理视图

|值|描述|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序应将此值传递给 方法，以 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 获取"**打开方式**"对话框（本例中为可能的代码视图）。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>处理程序将此值传递给 方法，以便获取"打开方式"对话框，在这种情况下，会填充映射到 与 相同的视图的可能调试 `cmdidOpenWith` <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>  <xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid> 视图 <xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid> 。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Designer_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序将此值传递给 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 方法，以便获取"**打开方式**"对话框，本例中为 **"查看窗体设计器视图**"。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Primary_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>处理程序将此值传递给 方法，以便获取"打开方式"对话框，在这种情况下，编辑器工厂 `cmdidOpenWith` <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 的默认/主视图。 |
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.TextView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>处理程序将此值传递给 方法，以便获取文档或数据文本编辑器视图的"打开方式 `cmdidOpenWith` <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> "对话框。 |
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.UserChooseView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序将此值传递给 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 方法，该方法会提示用户选择使用哪个用户定义的视图。|

## <a name="editor-factory-flags"></a>编辑器工厂标志

|值|描述|
|-----------|-----------------|
|[Cef。CloneFile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>)|已过时的标志将位组合为 方法的第一 <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> 个参数。|
|[Cef。OpenAsNew](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenAsNew>)|按位组合为 方法的第一个参数，这表示编辑器 <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> 工厂应执行必要的修复。|
|[Cef。OpenFile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenFile>)|此标志作为 方法的第一个参数进行组合，与 <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> CEF 互 [斥。CloneFile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>)。|
|[Cef。沉默](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_Silent>)|按位组合为 方法的第一个参数，这表示编辑器工厂应创建编辑器，而不在 UI (<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> 用户界面) 。|

## <a name="visual-studio-errors"></a>Visual Studio错误

|值|描述|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_BUSY>|当有关对象已经繁忙时，接口返回异步行为的常量|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>|特定于"不兼容文档数据Visual Studio的 HRESULT 错误。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PACKAGENOTLOADED>|特定于包的 HRESULT Visual Studio指示"包未加载"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTALREADYEXISTS>|特定于项目的错误 HRESULT Visual Studio指示"项目已存在"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTMIGRATIONFAILED>|特定于项目配置的错误 HRESULT Visual Studio指示"项目配置失败"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTNOTLOADED>|特定于项目的错误 HRESULT Visual Studio指示"项目未加载"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONALREADYOPEN>|特定于解决方案的错误 HRESULT Visual Studio指示"解决方案已打开"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONNOTOPEN>|特定于解决方案的错误 HRESULT Visual Studio指示"解决方案未打开"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SPECIFYING_OUTPUT_UNSUPPORTED>|由具有参数的生成接口返回，这些参数用于从接口指定数组，但实现只能将 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput> 方法应用于所有输出。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>|如果文档的格式无法在编辑器中打开，则 方法 <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> 返回此值。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_WIZARDBACKBUTTONPRESS>|一个 HRESULT 值，指示用户在向导中点击后退Visual Studio按钮。|

## <a name="visual-studio-constants"></a>Visual Studio常量

|值|描述|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_PROJECTFORWARDED>|特定于项目的错误 HRESULT Visual Studio指示"项目转发"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_TBXMARKER>|特定于"工具箱Visual Studio的常量。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_ENTERMODAL>|一个常量，Visual Studio方法广播通知消息，该方法指示 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> 形式开始。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_EXITMODAL>|一个常量，Visual Studio，用于通过指示形式结束的方法广播 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> 通知消息。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_TOOLBARMETRICSCHANGE>|一个常量，Visual Studio通过 方法广播通知消息， <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> 指示命令栏指标已更改。|
|<xref:Microsoft.VisualStudio.VSConstants.VSCOOKIE_NIL>|一个特定于 Visual Studio的常量，指示尚未设置 Cookie。|
|[VSITEMID。零](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Nil>)|一Visual Studio项标识符，表示缺少项目项。 如果没有当前选择，则使用此值。|
|[VSITEMID。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>)|一Visual Studio项标识符，它表示项目层次结构的根，用于标识整个层次结构，而不是单个项。|
|[VSITEMID。选择](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Selection>)|一Visual Studio项标识符，它表示当前选定的项，其中可以包含层次结构的根。|

## <a name="ivsselectionevents"></a>IVsSelectionEvents
 例如，描述刚刚在调用中选择了 IDE <xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents.OnElementValueChanged%2A> 的组件。

|返回的常量|Value|
|--------------|-----------|
|[SelectionElement.DocumentFrame](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_DocumentFrame>)|0x2|
|[SelectionElement.PropertyBrowserSID](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_PropertyBrowserSID>)|0x4|
|[SelectionElement.StartupProject](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_StartupProject>)|0x3|
|[SelectionElement.UndoManager](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UndoManager>)|0x0|
|[SelectionElement.UserContext](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UserContext>)|0x5|
|[SelectionElement.WindowFrame](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_WindowFrame>)|0x1|

## <a name="vsselelemid"></a>VSSELELEMID
 用于指示新选择状态常量。

|返回的常量|Value|
|--------------|-----------|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|2|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|7|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|4|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|6|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|3|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|0|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|5|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|1|

## <a name="component-selector-dialog-constants"></a>组件选择器对话常量

|返回的常量|Value|
|--------------|-----------|
|<xref:Microsoft.VisualStudio.VSConstants.CPDN_SELCHANGED>|WM_USER + 1280|
|<xref:Microsoft.VisualStudio.VSConstants.CPDN_SELDBLCLICK>|WM_USER + 1281|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_CLEARSELECTION>|WM_USER + 1290|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_GETSELECTION>|WM_USER + 1287|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_INITIALIZELIST>|WM_USER + 1285|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_INITIALIZETAB>|WM_USER + 1288|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_QUERYCANSELECT>|WM_USER + 1286|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_SETMULTISELECT>|WM_USER + 1289|

## <a name="see-also"></a>另请参阅

- [用于扩展项目系统的 IDE 定义命令](../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)
