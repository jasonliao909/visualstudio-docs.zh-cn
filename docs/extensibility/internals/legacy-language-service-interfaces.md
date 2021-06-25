---
title: 旧版语言服务接口|Microsoft Docs
description: 了解提供旧版语言服务功能的 Visual Studio SDK 中提供的接口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IVsLanguageInfo interface
- language services, objects
ms.assetid: 03b2d507-f463-417e-bc22-bdac68eeda52
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 75697e1d212b24b743fed62284b384985749fe7b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898599"
---
# <a name="legacy-language-service-interfaces"></a>旧版语言服务接口
对于任何特定编程语言，一次只能有一个语言服务实例。 但是，单个语言服务可以处理多个编辑器。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 不会将语言服务与任何特定编辑器关联。 因此，请求语言服务操作时，必须将相应的编辑器标识为参数。

## <a name="common-interfaces-associated-with-language-services"></a>与语言服务关联的常见接口
 编辑器通过调用相应的 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> VSPackage 获取语言服务。 在此调用中 (SID) ID 标识所请求的语言服务。

 可以在任意数目的单独类上实现核心语言服务接口。 但是，一种常见方法是在单个类中实现以下接口：

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageBlock>（可选）

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>必须在所有语言服务上实现 接口。 它提供有关语言服务的信息，例如语言的本地化名称、与语言服务关联的文件扩展名，以及如何检索着色器。

## <a name="additional-language-service-interfaces"></a>其他语言服务接口
 其他接口可以随语言服务一起提供。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 为文本缓冲区的每个实例请求这些接口的单独实例。 因此，应在其自己的 对象上实现其中每个接口。 下表显示了每个文本缓冲区实例需要一个实例的接口。

|接口|描述|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|管理代码窗口修饰，如下拉栏。 可以使用 方法获取此 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> 接口。 每个代码窗口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> 有一个。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>|为语言关键字和分隔符着色。 可以使用 方法获取此 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> 接口。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 在绘制时调用。 避免在 内部执行计算 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 密集型工作，否则性能可能会受到影响。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>|提供 IntelliSense 参数工具提示。 当语言服务识别指示应显示方法数据的字符（如打开的括号）时，它会调用 方法以通知文本视图语言服务已准备好显示参数 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> 信息工具提示。 然后，文本视图使用 接口的方法调用回语言服务，获取 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> 显示工具提示所需的信息。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>|提供 IntelliSense 语句完成。 当语言服务准备好显示完成列表时，它会对 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> 文本视图调用 方法。 然后，文本视图使用 对象上的方法调用回语言 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> 服务。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>|允许使用命令处理程序修改文本视图。 实现 接口的类 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> 还必须实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口。 文本视图通过查询传递到 方法中的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 对象来检索 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> 对象。 每个视图都应 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> 有一个对象。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|截获用户在代码窗口中输入的命令。 监视实现的输出 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 以提供自定义完成信息和视图修改<br /><br /> 若要将 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 对象传递给文本视图，请调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> 。|

## <a name="see-also"></a>另请参阅
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
- [清单：创建旧版语言服务](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)
