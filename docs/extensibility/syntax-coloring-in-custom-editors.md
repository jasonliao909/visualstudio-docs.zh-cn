---
title: 自定义编辑器中的语法着色|Microsoft Docs
description: 了解环境 SDK 自定义编辑器Visual Studio语法着色，该编辑器显示给定文档视图的指定颜色。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - syntax coloring
ms.assetid: 74900b9a-baef-432a-8231-4568fb5e19ad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 21710df4971581f95e82ff394b4880c262dd7bf3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122158107"
---
# <a name="syntax-coloring-in-custom-editors"></a>自定义编辑器中的语法着色
Visual Studio环境 SDK 编辑器（包括核心编辑器）使用语言服务来标识特定的语法项，并使用给定文档视图的指定颜色显示这些项。

## <a name="colorization-requirements"></a>着色要求
 实现语言服务着色器的所有编辑器都必须：

1. 使用实现 的对象来管理要着色的文本，并使用实现 的对象 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 来提供文本的文档视图。

2. 通过使用语言服务的标识 GUID 查询 VSPackage 的服务提供商，获取特定语言服务的接口。

3. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> 实现 的对象的 方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 。 此方法将语言服务与 VSPackage 用来管理要着色 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 的文本的实现关联。

## <a name="core-editor-usage-of-a-language-services-colorizer"></a>语言服务着色器的核心编辑器使用情况
 当具有着色器的语言服务由核心编辑器的实例获取时，语言服务的着色器会自动分析和呈现文本，而无需你进一步干预。

 IDE 以透明方式：

- 根据需要调用着色器，以分析和分析在 的实现中添加或修改的文本 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 。

- 确保使用着色器返回的信息更新和重新绘制实现提供的文档视图提供的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 显示。

## <a name="non-core-editor-usage-of-a-language-services-colorizer"></a>语言服务着色器的非核心编辑器用法
 非核心编辑器实例也可使用语言服务的语法着色服务，但它们必须显式检索和应用服务的着色器，并自行重新绘制其文档视图。

 为此，非核心编辑器必须：

1. 获取语言服务的着色器对象 (实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2>) 。 VSPackage 通过调用语言服务 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> 接口上的 方法实现此要求。

2. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 方法以请求对文本的特定范围进行着色。

     <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>方法返回一个值数组，一个数组用于要着色的文本范围中的每个字母。 它还将文本范围标识为可着色项的特定类型，例如注释、关键字或数据类型。

3. 使用 返回的着色信息 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 重新绘制并显示其文本。

> [!NOTE]
> 除了使用语言服务的着色器，VSPackage 还可以选择使用常规用途Visual Studio环境 SDK 文本着色机制。 有关此机制详细信息，请参阅 [使用字体和颜色](/previous-versions/visualstudio/visual-studio-2015/extensibility/using-fonts-and-colors?preserve-view=true&view=vs-2015)。

## <a name="see-also"></a>请参阅

- [在旧版语言服务中进行语法着色](../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [实现语法着色](../extensibility/internals/implementing-syntax-coloring.md)
- [如何：使用内置的可着色项](../extensibility/internals/how-to-use-built-in-colorable-items.md)
- [自定义可着色项](../extensibility/internals/custom-colorable-items.md)