---
title: 单选项卡和多选项卡视图|Microsoft Docs
description: 了解如何在编辑器（如代码编辑器窗口和窗体设计器）中实现多选项卡视图。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - single and multi-tab views
ms.assetid: e3611704-349f-4323-b03c-f2b0a445d781
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: d03563fe84d8985ab1fd1b746a05cd0c8d43e485
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600841"
---
# <a name="single-and-multi-tab-views"></a>单选项卡和多选项卡视图
编辑器可以创建不同类型的视图。 一个示例是代码编辑器窗口，另一个示例是窗体设计器。

 多选项卡视图是包含多个选项卡的视图。 例如，HTML 编辑器底部有两个选项卡："设计"和"**源**"，每个选项卡是一个逻辑视图。 设计视图显示呈现的网页，而另一个视图显示构成网页的 HTML。

## <a name="accessing-physical-views"></a>访问物理视图
 物理视图承载文档视图对象，每个对象表示缓冲区中数据的视图，例如代码或窗体。 因此，每个文档视图对象都有一个物理视图 (由称为物理视图字符串对象) 标识的物理视图对象，通常是单个逻辑视图。

 但在某些情况下，物理视图可以有两个或多个逻辑视图。 一些示例包括具有并行视图的拆分窗口的编辑器，或具有 GUI/设计视图和代码隐藏窗体视图的窗体设计器。

 若要使编辑器能够访问所有可用的物理视图，必须为编辑器工厂可以创建的每种类型的文档视图对象创建唯一的物理视图字符串。 例如，编辑器 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 工厂可以创建代码窗口和窗体设计器窗口的文档视图对象。

## <a name="creating-multi-tabbed-views"></a>创建多选项卡视图
 尽管文档视图对象必须通过唯一的物理视图字符串与物理视图相关联，但可以在物理视图中放置多个选项卡，以便以不同方式查看数据。 在此多选项卡配置中，所有选项卡都与同一物理视图字符串相关联，但每个选项卡都有不同的逻辑视图 GUID。

 若要为编辑器创建多选项卡视图，请实现 接口，然后将不同的逻辑视图 GUID () 与创建的每个 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiViewDocumentView> <xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID> 选项卡关联。

 HTML Visual Studio是具有多选项卡视图的编辑器示例。 它具有 **"设计"和****"源"** 选项卡。 若要启用此功能，每个选项卡、"设计"选项卡和"源"选项卡 `LOGICALVIEWID_TextView` 都有 `LOGICALVIEWID_Code` **一个不同的逻辑** 视图关联。

 通过指定适当的逻辑视图，VSPackage 可以访问与特定用途对应的视图，例如设计窗体、编辑代码或调试代码。 但是，其中一个窗口必须由 NULL 字符串标识，并且它必须对应于主逻辑视图 `LOGVIEWID_Primary` () 。

 下表列出了可用的逻辑视图值及其用途。

|LOGVIEWID GUID|推荐使用|
|--------------------|---------------------|
|`LOGVIEWID_Primary`|编辑器工厂的默认/主视图。<br /><br /> 所有编辑器工厂都必须支持此值。 此视图必须使用 NULL 字符串作为其物理视图字符串。 必须至少将一个逻辑视图设置为此值。|
|`LOGVIEWID_Debugging`|调试视图。 通常， `LOGVIEWID_Debugging` 映射到与 相同的视图 `LOGVIEWID_Code` 。|
|`LOGVIEWID_Code`|视图由"查看 **代码"命令** 启动。|
|`LOGVIEWID_Designer`|视图由"视图 **窗体"命令** 启动。|
|`LOGVIEWID_TextView`|文本编辑器视图。 这是返回 的视图 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> ，你可以从该视图访问 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。|
|`LOGVIEWID_UserChooseView`|提示用户选择使用哪个视图。|
|`LOGVIEWID_ProjectSpecificEditor`|由" **打开时"** 对话框传递到<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.OpenItem%2A><br /><br /> 当用户选择"默认编辑器 (Project") 时。|

 尽管逻辑视图 GUID 是可扩展的，但只能使用 VSPackage 中定义的逻辑视图 GUID。

 关闭时，Visual Studio将保留编辑器工厂的 GUID 和与文档窗口关联的物理视图字符串，以便可以在解决方案重新打开时用于重新打开文档窗口。 只有关闭解决方案时打开的窗口才持久保存于解决方案 (.suo) 文件中。 这些值对应于 在 `VSFPROPID_guidEditorType` 方法 `VSFPROPID_pszPhysicalView` 的 参数 `propid` 中传递的 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> 值。

## <a name="example"></a>示例
 此代码片段演示如何使用 <xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID.TextView> 对象访问实现 的视图 `IVsCodeWindow` 。 在这种情况下，服务 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument> 用于调用 和 请求 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A> `LOGVIEWID_TextView` ，这将获取指向窗口框架的指针。 通过调用 并指定 值来获取指向文档视图对象的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> 指针 `VSFPROPID_DocView` 。 从文档视图对象中， `QueryInterface` 为 调用 `IVsCodeWindow` 。 在这种情况下，预期返回文本编辑器，因此方法中返回的文档视图对象 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> 是代码窗口。

```cpp
HRESULT CFindTool::GotoFileLocation(const WCHAR * szFile, long iLine, long iStart, long iLen)
{
  HRESULT hr;
  if (NULL == szFile || !*szFile)
    return E_INVALIDARG;

  if (iLine == -1L)
    return S_FALSE;

  VSITEMID                  itemid;
  VARIANT                   var;
  RECT                      rc;
  IVsUIShellOpenDocument *  pOpenDoc    = NULL;
  IVsCodeWindow *           pCodeWin    = NULL;
  IVsTextView *             pTextView   = NULL;
  IVsUIHierarchy *          pHierarchy  = NULL;
  IVsWindowFrame *          pFrame      = NULL;
  IUnknown *                pUnk        = NULL;
  IVsHighlight *            pHighlight  = NULL;

  IfFailGo(CGlobalServiceProvider::HrQueryService(SID_SVsUIShellOpenDocument, IID_IVsUIShellOpenDocument, (void **)&pOpenDoc));
  IfFailGo(pOpenDoc->OpenDocumentViaProject(szFile, LOGVIEWID_TextView, NULL, &pHierarchy, &itemid, &pFrame));
  pFrame->Show();
  VariantInit(&var);
  IfFailGo(pFrame->GetProperty(VSFPROPID_DocView, &var));
  if (VT_UNKNOWN != var.vt) { hr = E_FAIL; goto Error; }
  pUnk = V_UNKNOWN(&var);
  if (NULL != pUnk)
  {
    IfFailGo(pUnk->QueryInterface(IID_IVsCodeWindow, (void **)&pCodeWin));
    if (SUCCEEDED(hr = pCodeWin->GetLastActiveView(&pTextView)) ||
        SUCCEEDED(hr = pCodeWin->GetPrimaryView(&pTextView)) )
    {
      pTextView->SetSelection(iLine, iStart, iLine, iStart + iLen);
      // uncover selection
      IfFailGo(pTextView->QueryInterface(IID_IVsHighlight, (void**)&pHighlight));
      IfFailGo(SUCCEEDED(pHighlight->GetHighlightRect(&rc)));
      UncoverSelectionRect(&rc);
    }
  }

Error:
  CLEARINTERFACE(pHighlight);
  CLEARINTERFACE(pTextView);
  CLEARINTERFACE(pCodeWin);
  CLEARINTERFACE(pUnk);
  CLEARINTERFACE(pFrame);
  CLEARINTERFACE(pOpenDoc);
  CLEARINTERFACE(pHierarchy);
  RedrawWindow(m_hwndResults, NULL, NULL, RDW_ERASE|RDW_FRAME|RDW_INVALIDATE|RDW_ALLCHILDREN);
  return hr;
}
```

## <a name="see-also"></a>另请参阅
- [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)
- [如何：将视图附加到文档数据](../extensibility/how-to-attach-views-to-document-data.md)
- [创建自定义编辑器和设计器](../extensibility/creating-custom-editors-and-designers.md)
