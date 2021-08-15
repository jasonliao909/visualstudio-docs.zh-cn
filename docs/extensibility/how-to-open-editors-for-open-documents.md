---
title: 如何：打开用于打开文档的编辑器|Microsoft Docs
description: 了解如何在标准编辑器或特定于项目的编辑器中打开文件。 项目打开文档窗口时，必须确定文件是否已打开。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], opening for open documents
ms.assetid: 1a0fa49c-efa4-4dcc-bdc0-299b7052acdc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: bcc01a90c058e53a461b3e5d21d9f11fe0cd8c18d0ac84ee9b90e6154feee7fd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432684"
---
# <a name="how-to-open-editors-for-open-documents"></a>如何：打开打开的文档的编辑器
在项目打开文档窗口之前，项目首先必须确定该文件是否已在文档窗口中打开，以便其他编辑器使用。 可以在特定于项目的编辑器中打开该文件，也可以打开注册到 的标准编辑器之一 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

## <a name="open-a-project-specific-editor"></a>打开特定于项目的编辑器
 使用以下过程为已打开的文件打开特定于项目的编辑器。

### <a name="to-open-a-project-specific-editor-for-an-open-file"></a>为打开的文件打开特定于项目的编辑器

1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> 方法。

    此调用将返回指向文档的层次结构、层次结构项和窗口框架的指针（如果适用）。

2. 如果文档已打开，则项目必须检查是否仅存在文档数据对象，或者是否也存在文档视图对象。

   - 如果文档视图对象存在，并且此视图用于其他层次结构或层次结构项，则项目将使用指向视图窗口框架的指针来重新显示现有窗口。

   - 如果文档视图对象存在，并且此视图用于同一层次结构和层次结构项，则项目可以打开第二个视图（如果它可以附加到基础文档数据对象）。 否则，项目应该使用指向视图窗口框架的指针来重新显示现有窗口。

   - 如果只有文档数据对象存在，则项目应确定它是否可以将文档数据对象用于其视图。 如果文档数据对象兼容，请完成打开特定于项目的编辑器 [中讨论的步骤](../extensibility/how-to-open-project-specific-editors.md)。

     如果文档数据对象不兼容，则应该向用户显示一个错误，指示该文件当前正在使用。 此错误应仅在暂时性情况下显示，例如，当用户尝试使用核心文本编辑器而不是编辑器打开文件时，正在编译 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 文件。 核心文本编辑器可以与编译器共享文档数据对象。

3. 如果文档因没有文档数据对象或文档视图对象而未打开，请完成打开特定于 [项目的编辑器 中的步骤](../extensibility/how-to-open-project-specific-editors.md)。

## <a name="open-a-standard-editor"></a>打开标准编辑器
 使用以下过程打开已打开的文件的标准编辑器。

### <a name="to-open-a-standard-editor-for-an-open-file"></a>打开打开文件的标准编辑器

1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>。

     此方法首先通过调用 来验证文档是否尚未打开 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> 。 如果文档已打开，则其编辑器窗口将重新显示。

2. 如果文档未打开，请完成如何：打开标准 [编辑器 中的步骤](../extensibility/how-to-open-standard-editors.md)。

## <a name="see-also"></a>另请参阅
- [打开并保存项目项](../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开特定于项目的编辑器](../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开标准编辑器](../extensibility/how-to-open-standard-editors.md)
