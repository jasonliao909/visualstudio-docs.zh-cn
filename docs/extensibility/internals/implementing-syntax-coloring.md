---
title: 实现语法着色|Microsoft Docs
description: 了解如何使用 MPF Visual Studio托管包框架的语言服务功能在 (中实现语法) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- syntax coloring, implementing
- editors [Visual Studio SDK], colorizing text
- text, colorizing in editors
ms.assetid: 96e762ca-efd0-41e7-8958-fda4897c8c7a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 8170ed2791d746bc167f23d6b30c251aa731b129c2a153a4bae99af5ccf8a7f0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121375945"
---
# <a name="implementing-syntax-coloring"></a>实现语法着色
当语言服务提供语法着色时，分析器会将文本行转换为可着色项数组，并返回对应于这些可着色项的标记类型。 分析器应返回属于可着色项列表的标记类型。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 根据着色器对象分配给相应标记类型的属性，在代码窗口中显示每个可着色项。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 未指定分析器接口，分析器实现完全由你决定。 但是，语言包项目中提供了默认Visual Studio实现。 对于托管代码，MPF (包框架) 为文本着色提供完全支持。

 旧版语言服务作为 VSPackage 的一部分实现，但实现语言服务功能的较新方式是使用 MEF 扩展。 若要详细了解实现语法着色的新方法，请参阅 [演练：突出显示文本](../../extensibility/walkthrough-highlighting-text.md)。

> [!NOTE]
> 建议尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并让你能够利用新的编辑器功能。

## <a name="steps-followed-by-an-editor-to-colorize-text"></a>编辑器为文本着色后的步骤

1. 编辑器通过调用 对象上的 方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> 获取着色 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> 器。

2. 编辑器调用 方法，以确定着色器是否需要在着色器外部维护每行 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStateMaintenanceFlag%2A> 的状态。

3. 如果着色器要求在着色器外部维护状态，编辑器将调用 方法来 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStartState%2A> 获取第一行的状态。

4. 对于缓冲区的每一行，编辑器将调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 方法，该方法执行以下步骤：

    1. 将文本行传递给扫描程序，以将文本转换为标记。 每个标记指定令牌文本和标记类型。

    2. 标记类型将转换为可着色项列表的索引。

    3. 标记信息用于填充数组，使数组的每个元素对应于行中的字符。 数组中存储的值是可着色项列表中的索引。

    4. 每行都返回行尾的状态。

5. 如果着色器需要维护状态，编辑器将缓存该行的状态。

6. 编辑器使用从 方法返回的信息呈现文本 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 行。 这需要执行以下步骤：

    1. 对于行中的每个字符，获取可着色项索引。

    2. 如果使用默认的可着色项，则访问编辑器的可着色项列表。

    3. 否则，请调用语言服务的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> 方法以获取可着色项。

    4. 使用可着色项中的信息将文本呈现到显示中。

## <a name="managed-package-framework-colorizer"></a>托管包框架着色器
 MPF (包) 提供了实现着色器所需的所有类。 语言服务类应继承 <xref:Microsoft.VisualStudio.Package.LanguageService> 类，并实现所需的方法。 必须通过实现 接口提供扫描程序和分析器，然后从 方法返回该接口的实例 (必须在 类中实现的方法之 <xref:Microsoft.VisualStudio.Package.IScanner> <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> 一) 。 有关详细信息，请参阅 [旧版语言服务 中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)。

## <a name="see-also"></a>请参阅
- [如何：使用内置的可着色项](../../extensibility/internals/how-to-use-built-in-colorable-items.md)
- [自定义可着色项](../../extensibility/internals/custom-colorable-items.md)
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)
