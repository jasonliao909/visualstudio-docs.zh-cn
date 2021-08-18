---
title: 自定义编辑器中的文档数据和文档|Microsoft Docs
description: 了解自定义编辑器的组件，这些组件是文档数据对象和文档视图对象。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document data and document view
ms.assetid: 71eea623-f566-4feb-84cd-ca1ba71bc493
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 5cee92e4831b1639293064f6776430359eebefb0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122152518"
---
# <a name="document-data-and-document-view-in-custom-editors"></a>自定义编辑器中的文档数据和文档视图
自定义编辑器由两部分组成：文档数据对象和文档视图对象。 如名称所建议，文档数据对象表示要显示的文本数据。 同样，文档视图对象 (或"view") 表示一个或多个窗口，用于显示文档数据对象。

## <a name="document-data-object"></a>文档数据对象
 文档数据对象是文本缓冲区中文本的数据表示形式。 它是一个 COM 对象，用于存储文档文本和其他信息。 文档数据对象还处理文档持久性，并启用其数据的多个视图。 有关详细信息，请参阅

 <xref:EnvDTE80.Window2.DocumentData%2A>和[Document Windows。](../extensibility/internals/document-windows.md)

 自定义编辑器和设计器可以选择使用 对象 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 或自己的自定义缓冲区。 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 遵循标准编辑器的简化嵌入模型，支持多个视图，并提供用于管理多个视图的事件接口。

## <a name="document-view-object"></a>文档视图对象
 显示代码和其他文本的窗口称为文档视图或视图。 创建编辑器时，可以选择单个视图，其中文本显示在单个窗口中。 或者，可以选择多个视图，其中文本显示在多个窗口中。 你的选择取决于你的应用程序。 例如，如果需要并行编辑，可以选择多个视图。 每个视图都与集成开发环境 (IDE 中的条目相关联) RDT (文档) 。 视图窗口属于项目或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 对象。

 如果编辑器支持文档数据对象的多个视图，则文档数据和文档视图对象必须分开。 否则，可以组合在一起。 有关详细信息，请参阅 [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)。

 例如，当包含文档的解决方案关闭) 时， (IDE 通过为正在运行的文档表中的每个条目匹配项标识符 (ItemID) 来通知有关事件视图。 有关此内容详细信息，请参阅 [运行文档表](../extensibility/internals/running-document-table.md)。

 有两个选项用于创建自定义编辑器的视图。 一种是就地激活模型，其中视图使用 ActiveX 控件或文档数据对象托管在窗口中。 第二种是简化的嵌入模型，其中视图由 承载， [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> 并实现以处理窗口命令。 有关就地激活模型的信息，请参阅 [就地激活](/previous-versions/visualstudio/visual-studio-2015/misc/in-place-activation?preserve-view=true&view=vs-2015)。 有关简化的嵌入模型的信息，请参阅 [简化的嵌入](../extensibility/simplified-embedding.md)。

## <a name="see-also"></a>请参阅

- [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)
- [简化的嵌入](../extensibility/simplified-embedding.md)
- [如何：将视图附加到文档数据](../extensibility/how-to-attach-views-to-document-data.md)
- [文档锁持有者管理](../extensibility/document-lock-holder-management.md)
- [单选项卡视图和多选项卡视图](../extensibility/single-and-multi-tab-views.md)
- [保存标准文档](../extensibility/internals/saving-a-standard-document.md)
- [持久性和正在运行的文档表](../extensibility/internals/persistence-and-the-running-document-table.md)
- [确定哪个编辑器在项目中打开文件](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)