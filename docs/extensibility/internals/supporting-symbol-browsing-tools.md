---
title: 支持 Symbol-Browsing 工具 |Microsoft Docs
description: Visual Studio 提供 Visual Studio 中的符号浏览功能。 了解如何在组件中将这些功能与库进行扩展。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- symbols, symbol-browsing tools
- browsers, symbol browsers
- symbol-browsing tools
- libraries
- IVsLibrary2 interface, symbol-browsing tools
- IVsSimpleLibrary2 interface, symbol-browsing tools
- symbol-browsing tools, library manager
- symbols
- libraries, symbol-browsing tools
ms.assetid: 70d8c9e5-4b0b-4a69-b3b3-90f36debe880
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 560134da26f7123da56426caaa06641cfacd64103c05f6fe681eb7aa34f47ba5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414204"
---
# <a name="supporting-symbol-browsing-tools"></a>支持符号浏览工具
**对象浏览器**、**类视图**、**调用浏览器** 和 **查找符号结果** 工具在 Visual Studio 中提供符号浏览功能。 这些工具显示符号的分层树视图，并显示树中符号之间的关系。 符号可以表示各个组件中包含的命名空间、对象、类、类成员和其他语言元素。 组件包括 Visual Studio 项目、外部 .NET Framework 组件以及类型 ( .tlb) 库。 有关详细信息，请参阅 [查看代码的结构](../../ide/viewing-the-structure-of-code.md)。

## <a name="symbol-browsing-libraries"></a>Symbol-Browsing 库
 作为语言实施者，可以通过创建跟踪组件中符号的库，并通过一组接口向 Visual Studio 对象管理器提供符号列表，来扩展 Visual Studio 符号浏览功能。 库由 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2> 接口描述。 Visual Studio 对象管理器通过从库中获取数据并对其进行组织，来响应来自符号浏览工具的新数据请求。 然后，它会用请求的数据填充或更新工具。 若要获取对 Visual Studio 对象管理器的引用， <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2> 请将 <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> 服务 ID 传递到 `GetService` 方法。

 每个库都必须注册到 Visual Studio 对象管理器，该对象管理器会收集所有库中的信息。 若要注册库，请调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> 方法。 根据哪个工具启动请求，Visual Studio 对象管理器将查找相应的库并请求数据。 数据 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 在接口所描述的符号列表中在库和对象管理器之间传输 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> 。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]对象管理器负责定期刷新符号浏览工具，以反映库中包含的最新数据。

 下图包含库和 Visual Studio 对象管理器之间的请求/数据交换过程的关键元素示例。 关系图中的接口是托管代码应用程序的一部分。

 ![库与对象管理器间的数据流](../../extensibility/internals/media/callbrowserdiagram.gif "CallBrowserDiagram")

 若要向 Visual Studio 对象管理器提供符号列表，必须先通过调用方法向 Visual Studio 对象管理器注册库 <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> 。 库注册完成后，Visual Studio 对象管理器将请求某些有关库功能的信息。 例如，它通过调用和方法请求库标志和支持的类别 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetLibFlags2%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetSupportedCategoryFields2%2A> 。 在某些时候，当某个工具请求此库中的数据时，对象管理器将通过调用方法来请求顶级符号列表 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetList2%2A> 。 作为响应，库会制造符号列表，并通过接口将其公开给 Visual Studio 对象管理器 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> 。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]对象管理器通过调用方法来确定列表中有多少项 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetItemCount%2A> 。 所有以下请求都与列表中的给定项相关，并提供每个请求中的项索引号。 Visual Studio 对象管理器将通过调用方法继续收集有关该项目的类型、辅助功能和其他属性的信息 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetCategoryField2%2A> 。

 它通过调用方法来确定项的名称 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetTextWithOwnership%2A> ，并通过调用方法来请求图标信息 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetDisplayData%2A> 。 此图标显示在项名称的左侧，并描述项的类型、可访问性和其他属性。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]对象管理器调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetExpandable3%2A> 方法来确定给定列表项是否可展开并具有子项项。 如果 UI 发送请求来展开元素，则对象管理器将通过调用方法请求子符号列表 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetList2%2A> 。 该过程将继续，并以按需生成的树的不同部分为依据。

> [!NOTE]
> 若要实现本机代码符号提供程序，请使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsLibrary2> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectList2> 接口。

## <a name="see-also"></a>另请参阅
- [如何：使用对象管理器注册库](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [如何：向对象管理器公开库提供的符号列表](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
- [如何：识别库中的符号](../../extensibility/internals/how-to-identify-symbols-in-a-library.md)
