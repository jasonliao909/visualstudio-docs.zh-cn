---
title: 旧版语言服务中的语法着色|Microsoft Docs
description: 了解如何Visual Studio旧版语言服务中实现语法着色服务，以识别语言的元素，以及如何在编辑器中以颜色显示这些元素。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- syntax coloring
- language services, syntax coloring
ms.assetid: f65ff67e-8c20-497a-bebf-5e2a5b5b012f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 9fd4ef371756d27ff90e4445562065dd0c5bbe30ccae857018d0b1a6ff210722
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121431926"
---
# <a name="syntax-coloring-in-a-legacy-language-service"></a>在旧版语言服务中进行语法着色

Visual Studio使用着色服务来标识语言的元素，并使用编辑器中的指定颜色显示这些元素。

## <a name="colorizer-model"></a>着色器模型
 语言服务实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 接口，该接口随后由编辑器使用。 此实现是语言服务中的单独对象，如下图所示：

 ![SVC 着色程序图](../../extensibility/internals/media/figlgsvccolorizer.gif)

> [!NOTE]
> 语法着色服务独立于常规Visual Studio文本着色机制。 有关支持着色 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 的常规机制详细信息，请参阅 [使用字体和颜色](/previous-versions/visualstudio/visual-studio-2015/extensibility/using-fonts-and-colors?preserve-view=true&view=vs-2015)。

 除了着色器，语言服务还可以提供编辑器使用的自定义可着色项，其广告是它提供自定义可着色项。 为此，可以在实现 接口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> 的同一对象上实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> 接口。 它在编辑器调用 方法时返回自定义可着色项的数量，在编辑器调用 方法时返回单个 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> 自定义可着色 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> 项。

 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>方法返回实现 接口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> 的对象。 如果语言服务支持 24 位或高颜色值，则必须在接口的同一 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 对象上实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> 接口。

## <a name="how-a-vspackage-uses-a-language-service-colorizer"></a>VSPackage 如何使用语言服务着色器

1. VSPackage 必须获取相应的语言服务，这需要语言服务 VSPackage 执行以下操作：

    1. 使用实现 接口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 的对象获取要着色的文本。

         文本通常使用实现 接口的对象 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 显示。

    2. 通过查询语言服务 GUID 的 VSPackage 的服务提供商获取语言服务。 语言服务在注册表中按文件扩展名进行标识。

    3. 通过调用语言服务的方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> ，将语言服务与 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> 关联。

2. VSPackage 现在可以获取并使用着色器对象，如下所示：

    > [!NOTE]
    > 使用核心编辑器的 VSPackage 不必显式获取语言服务的着色器对象。 一旦核心编辑器的实例获取适当的语言服务，它就会执行此处显示的所有着色任务。

    1. 通过调用语言服务对象上的 方法，获取实现 和 接口的语言服务 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> 着色器 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> 对象。

    2. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 方法以获取特定文本跨度的着色器信息。

         <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 返回一个值数组，其中一个值用于要着色的文本范围中的每个字符。 这些值是可着色项列表的索引，可着色项列表是由核心编辑器维护的默认可着色项列表，或者是语言服务本身维护的自定义可着色项列表。

    3. 使用 方法返回的着色 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 信息显示所选文本。

> [!NOTE]
> 除了使用语言服务着色器，VSPackage 还可使用常规用途Visual Studio着色机制。 有关此机制的信息，请参阅 [使用字体和颜色](/previous-versions/visualstudio/visual-studio-2015/extensibility/using-fonts-and-colors?preserve-view=true&view=vs-2015)。

## <a name="in-this-section"></a>本节内容
- [实现语法着色](../../extensibility/internals/implementing-syntax-coloring.md)

 讨论编辑器如何访问语言服务的语法着色，以及语言服务必须实现哪些内容来支持语法着色。

- [如何：使用内置的可着色项](../../extensibility/internals/how-to-use-built-in-colorable-items.md)

 演示如何使用语言服务中的内置可着色项。

- [自定义可着色项](../../extensibility/internals/custom-colorable-items.md)

 讨论如何实现自定义可着色项。
