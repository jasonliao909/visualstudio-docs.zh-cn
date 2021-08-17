---
title: 在语言服务服务中提供大纲|Microsoft Docs
description: 了解如何通过添加编辑器控制的大纲区域以及客户端控制的大纲区域，在旧版语言服务中提供扩展的大纲支持。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], outlining support
- language services, supporting outlining
- outlining, supporting
ms.assetid: df759e89-8193-418c-8038-6626304d387b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f3360c51e1cc2e7bc7d9e2841fc2e6f0b1a98077
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122042386"
---
# <a name="how-to-provide-expanded-outlining-support-in-a-legacy-language-service"></a>如何：在旧版语言服务中提供扩展的大纲显示支持
除了支持"折叠到定义"命令外，还有两个选项可以扩展对语言的大纲 **显示** 支持。 可以添加编辑器控制的大纲区域，并添加客户端控制的大纲区域。

## <a name="adding-editor-controlled-outline-regions"></a>添加编辑器控制的大纲区域
 此方法用于创建大纲区域，然后允许编辑器处理区域是否展开、折叠等。 在提供大纲显示支持的两个选项中，此选项最不可靠。 对于此选项，使用 在指定的文本范围内创建新的大纲区域 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> 。 创建此区域后，其行为由编辑器控制。 使用以下过程实现编辑器控制的大纲区域。

### <a name="to-implement-an-editor-controlled-outline-region"></a>实现编辑器控制的大纲区域

1. 调用 `QueryService`<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>

     这会返回指向 的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> 。

2. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A> ，传递给定文本缓冲区的指针。 这会返回指向缓冲区 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> 对象的指针。

3. 为 <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> 指向 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> 的指针调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession> on。

4. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> 以一次添加一个或多个新的大纲区域。

     此方法允许你指定要大纲的文本范围、是删除还是保留现有的大纲区域，以及默认情况下是展开还是折叠大纲区域。

## <a name="add-client-controlled-outline-regions"></a>添加客户端控制的大纲区域
 使用这种方法实现客户端控制的 (智能) 和语言服务使用的大纲 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 。 管理自己的大纲显示的语言服务监视文本缓冲区内容，以便销毁旧的大纲区域（当它们失效时）并根据需要创建新的大纲区域。

### <a name="to-implement-a-client-controlled-outline-region"></a>实现客户端控制的大纲区域

1. 调用 `QueryService` <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> 。 这会返回指向 的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> 。

2. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A> ，传递给定文本缓冲区的指针。 这确定缓冲区的隐藏文本会话是否已存在。

3. 如果文本会话已存在，则无需创建一个，并返回指向现有对象的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> 指针。 使用此指针枚举和创建大纲区域。 否则， <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> 请调用 以创建缓冲区的隐藏文本会话。 返回指向 对象的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> 指针。

    > [!NOTE]
    > 调用 时 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> ，可以指定隐藏文本客户端 (，即 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient> 对象) 。 当用户展开或折叠隐藏文本或大纲区域时，此客户端会通知你。

4. 调用) 参数：在 结构的成员中指定 值，以指示正在创建大纲区域，而不是 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.HIDDEN_REGION_TYPE> `iType` <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> 隐藏区域。 指定区域是在 结构的成员中由客户端控制 `dwBehavior` 还是由编辑器 <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> 控制。 智能大纲显示实现可以包含编辑器和客户端控制的大纲区域的组合。 指定在大纲区域折叠时显示的横幅文本，例如结构成员中的 `pszBanner` <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> "..."。 编辑器隐藏区域的默认横幅文本为"..."。
