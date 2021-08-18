---
title: 如何：支持旧版语言服务中的大纲|Microsoft Docs
description: 了解如何在旧版语言服务中提供对不同文本区域进行大纲显示、展开或折叠的支持。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], collapse to definitions command
- language services, supporting Collapse to Definitions command
- hidden text, Collapse to Definitions command
ms.assetid: bb6e74c3-93e4-4ef7-afc7-1c9b342f083b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: cef8f5520ebd0034ff5d8852129b1f076bf53b28
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122050008"
---
# <a name="how-to-support-outlining-in-a-legacy-language-service"></a>如何：支持旧版语言服务中的大纲显示
大纲显示用于展开或折叠不同文本区域。 使用大纲显示的方式可以通过不同的语言以不同方式定义。 有关详细信息，请参阅[大纲显示](../../ide/outlining.md)。

 旧版语言服务作为 VSPackage 的一部分实现，但实现语言服务功能的较新方式是使用 MEF 扩展。 若要详细了解实现大纲显示的新方法，请参阅 [演练：大纲显示](../../extensibility/walkthrough-outlining.md)。

> [!NOTE]
> 建议尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并让你能够利用新的编辑器功能。

 下面演示如何为语言服务支持此命令。

## <a name="to-support-outlining"></a>支持大纲显示

1. 在 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage> 语言服务对象上实现 。

2. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> 当前大纲显示会话对象以添加新大纲区域。

## <a name="robust-programming"></a>可靠编程
 当用户在"**大纲显示"** 菜单上选择"折叠到定义"时，IDE 会调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage.CollapseToDefinitions%2A> 语言服务。

 调用此方法时，IDE 将传递一个指针， (指向文本缓冲区的指针) 将指针 (指向当前大纲显示会话的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession>) 。

 可以通过在 参数中指定这些区域，为多个大纲区域 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> 调用 `rgOutlnReg` 方法。 参数 `rgOutlnReg` 是一个 <xref:Microsoft.VisualStudio.TextManager.Interop.NewOutlineRegion> 结构。 此过程允许指定隐藏区域的不同特征，例如特定区域是展开还是折叠。

> [!NOTE]
> 请谨慎隐藏换行符。 隐藏文本应从第一行的开始处扩展到节中最后一行的最后一个字符，使最后一个换行符可见。

## <a name="see-also"></a>请参阅
- [如何：在旧版语言服务中提供隐藏文本支持](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)
- [如何：在旧版语言服务中提供扩展的大纲显示支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)
