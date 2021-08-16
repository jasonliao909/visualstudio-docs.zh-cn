---
title: 旧版语言服务中的快速|Microsoft Docs
description: 了解 IntelliSense 快速信息操作对显示有关标识符的信息的支持。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Quick Info, supporting in language services [managed package framework]
- IntelliSense, Quick Info
- language services [managed package framework], IntelliSense Quick Info
ms.assetid: 159ccb0b-f5d6-4912-b88b-e9612924ed5e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 2c8a9b09ac8ad7391336816f4416a25ebd98484badb21ff81e1ec4604784eead
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414462"
---
# <a name="quick-info-in-a-legacy-language-service"></a>旧版语言服务中的快速信息
当用户将插入点置于标识符中，然后从 IntelliSense 菜单中选择"快速信息"或将鼠标光标悬停在标识符上时 **，IntelliSense** 快速信息会显示有关源中标识符的信息。 这会导致显示工具提示，并包含有关标识符的信息。 此信息通常由标识符类型组成。 当调试引擎处于活动状态时，此信息可能包括当前值。 调试引擎提供表达式值 ，而语言服务仅处理标识符。

 旧版语言服务作为 VSPackage 的一部分实现，但实现语言服务功能的较新方式是使用 MEF 扩展。 若要了解更多信息，请参阅 [演练：显示 QuickInfo 工具提示](../../extensibility/walkthrough-displaying-quickinfo-tooltips.md)。

> [!NOTE]
> 建议尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并让你能够利用新的编辑器功能。

 MPF (语言) 的托管包框架完全支持显示 IntelliSense 快速信息工具提示。 你不得不提供要显示的文本并启用快速信息功能。

 通过调用具有 分析原因值 的方法 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 分析器来获取要显示的文本 <xref:Microsoft.VisualStudio.Package.ParseReason> 。 此原因告知分析器获取类型信息 (或适用于在 对象中指定位置的标识符) 快速信息工具提示中显示的任何 <xref:Microsoft.VisualStudio.Package.ParseRequest> 内容。 <xref:Microsoft.VisualStudio.Package.ParseRequest>对象是传递给 方法 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 的对象。

 分析器必须分析对象中所有内容的位置， <xref:Microsoft.VisualStudio.Package.ParseRequest> 以确定所有标识符的类型。 然后，分析器必须在分析请求位置获取标识符。 最后，分析器必须将与该标识符关联的工具提示数据传递给 对象，以便 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 对象可以从 方法返回 <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A> 文本。

## <a name="enabling-the-quick-info-feature"></a>启用快速信息功能
 若要启用"快速信息"功能，必须设置 `CodeSense` `QuickInfo` 的 和命名参数 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 。这些属性设置 和 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableQuickInfo%2A> 属性。

## <a name="implementing-the-quick-info-feature"></a>实现快速信息功能
 类 <xref:Microsoft.VisualStudio.Package.ViewFilter> 处理 IntelliSense 快速信息操作。 当 类收到 命令时，类将调用 方法，其分析原因为 ，在发送命令时为 <xref:Microsoft.VisualStudio.Package.ViewFilter> <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> <xref:Microsoft.VisualStudio.Package.ParseReason> caret <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> 的位置。 然后，方法分析器必须分析源到给定位置，然后分析给定位置的标识符，以确定要显示在"快速信息" <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 工具提示中的内容。

 大多数分析器对整个源文件进行初始分析，将结果存储在分析树中。 将 传递到 方法时， <xref:Microsoft.VisualStudio.Package.ParseReason> 将执行完整的 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 分析。 然后，其他类型的分析可以使用分析树来获取所需信息。

 例如， 的分析原因值可以在源位置查找标识符，在分析树中查找它 <xref:Microsoft.VisualStudio.Package.ParseReason> 以获取类型信息。 然后，此类型信息将传递给 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 类，由 方法 <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A> 返回。
