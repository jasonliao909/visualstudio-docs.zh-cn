---
title: 支持 Symbol-Browsing Tools |Microsoft Docs
description: Visual Studio中提供符号浏览Visual Studio。 了解如何使用组件中的符号库扩展这些功能。
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
ms.openlocfilehash: 9b8383158773e088b1bfd2e5c955ff224c6800ad
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122158900"
---
# <a name="supporting-symbol-browsing-tools"></a>支持符号浏览工具
**对象浏览器****、类视图、调用浏览器** 和 **查找符号结果** 工具在 Visual Studio 中提供符号浏览功能。 这些工具显示符号的分层树视图，并显示树中符号之间的关系。 符号可以表示各种组件中包含的命名空间、对象、类、类成员和其他语言元素。 组件包括Visual Studio项目、外部.NET Framework组件和类型 (.tlb) 库。 有关详细信息，请参阅 [查看代码 的结构](../../ide/viewing-the-structure-of-code.md)。

## <a name="symbol-browsing-libraries"></a>Symbol-Browsing库
 作为语言实现者，可以通过创建用于跟踪组件中的符号并通过一组接口向 Visual Studio 对象管理器提供符号列表的库来扩展 Visual Studio 符号浏览功能。 库由 接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2> 描述。 对象Visual Studio通过从库中获取数据并组织它来响应来自符号浏览工具的新数据请求。 随后，它会使用请求的数据填充或更新工具。 若要获取对对象Visual Studio的引用，请 <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2> 将 <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> 服务 ID 传递给 `GetService` 方法。

 每个库都必须注册到Visual Studio管理器，该管理器将收集有关所有库的信息。 若要注册库，请调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> 方法。 根据启动请求的工具，Visual Studio管理器查找相应的库并请求数据。 数据在库和对象管理器之间传输 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，这些符号列表由 接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> 描述。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]对象管理器负责定期刷新符号浏览工具，以反映库中包含的最新数据。

 下图包含库与对象管理器之间的请求/数据交换过程Visual Studio示例。 关系图中的接口是托管代码应用程序的一部分。

 ![库与对象管理器间的数据流](../../extensibility/internals/media/callbrowserdiagram.gif "CallBrowserDiagram")

 若要向对象管理器Visual Studio符号列表，必须先通过调用 Visual Studio 向对象管理器注册 <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> 库。 注册库后，Visual Studio管理器将请求有关库功能的某些信息。 例如，它通过调用 和 方法来请求库标志和支持 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetLibFlags2%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetSupportedCategoryFields2%2A> 的类别。 在某些时候，当其中一个工具请求来自此库的数据时，对象管理器会通过调用 方法请求符号的顶级 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetList2%2A> 列表。 作为响应，库会创建一个符号列表，并通过 接口Visual Studio对象管理器 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> 公开该列表。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]对象管理器通过调用 方法确定列表中有多少 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetItemCount%2A> 项。 以下所有请求都与列表中的给定项相关，并在每个请求中提供项索引号。 对象Visual Studio通过调用 方法来收集有关项的类型、可访问性和其他属性 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetCategoryField2%2A> 的信息。

 它通过调用 方法确定项的名称，并 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetTextWithOwnership%2A> 调用 方法请求图标 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetDisplayData%2A> 信息。 图标显示在项名称的左侧，并描述项的类型、辅助功能和其他属性。

 对象 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 管理器调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetExpandable3%2A> 方法，以确定给定的列表项是否可展开并且具有子项。 如果 UI 发送展开元素的请求，则对象管理器通过调用 方法请求符号的子 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetList2%2A> 列表。 该过程继续进行，并按需生成树的不同部分。

> [!NOTE]
> 若要实现本机代码符号提供程序，请使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsLibrary2> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectList2> 接口。

## <a name="see-also"></a>请参阅
- [如何：使用对象管理器注册库](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [如何：向对象管理器公开库提供的符号列表](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
- [如何：识别库中的符号](../../extensibility/internals/how-to-identify-symbols-in-a-library.md)
