---
title: 如何：将视图附加到文档数据|Microsoft Docs
description: 可以将新的文档视图附加到现有文档数据对象。 使用此过程确定是否可以附加视图。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], custom - attach views to document data
ms.assetid: f92c0838-45be-42b8-9c55-713e9bb8df07
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 4171f80f3dc63fb00a64fc99c3620771ea8c48c4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600777"
---
# <a name="how-to-attach-views-to-document-data"></a>如何：将视图附加到文档数据
如果有新的文档视图，可以将其附加到现有文档数据对象。

## <a name="to-determine-if-you-can-attach-a-view-to-an-existing-document-data-object"></a>确定是否可以将视图附加到现有文档数据对象

1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>。

2. 在 的实现中，当 IDE 调用实现时，对现有的 `IVsEditorFactory::CreateEditorInstance` `QueryInterface` 文档数据对象调用 `CreateEditorInstance` 。

    通过 `QueryInterface` 调用 ，可以检查参数中指定的现有文档数据 `punkDocDataExisting` 对象。

    但是，必须查询的确切接口取决于打开文档的编辑器，如步骤 4 所述。

3. 如果找不到现有文档数据对象上的相应接口，则向编辑器返回错误代码，指示文档数据对象与编辑器不兼容。

    在 IDE 的 实现中，消息框会通知你文档在另一个编辑器中打开，并询问 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 是否要关闭它。

4. 如果关闭此文档，Visual Studio次调用编辑器工厂。 在此调用中， `DocDataExisting` 参数等于 NULL。 然后，编辑器工厂实现可以在自己的编辑器中打开文档数据对象。

   > [!NOTE]
   > 若要确定是否可以使用现有文档数据对象，还可以将指针强制转换到专用实现的实际类，从而使用接口实现 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] 方面的私有知识。 例如，所有标准编辑器都实现 `IVsPersistFileFormat` ，它继承自 <xref:Microsoft.VisualStudio.OLE.Interop.IPersist> 。 因此，可以调用 ，如果现有文档数据对象的类 ID 与实现类 ID 匹配，则您可以使用 `QueryInterface` <xref:Microsoft.VisualStudio.OLE.Interop.IPersist.GetClassID%2A> 文档数据对象。

## <a name="robust-programming"></a>可靠编程
 当Visual Studio调用 方法的实现时，它会传递回指向 参数中现有文档数据对象的指针（ <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> `punkDocDataExisting` 如果存在）。 检查 中返回的文档数据对象，以确定文档数据对象是否适合编辑器，如本主题过程的步骤 4 中的说明 `punkDocDataExisting` 所述。 如果合适，则编辑器工厂应为数据提供第二个视图，如支持多个文档 [视图 所述](../extensibility/supporting-multiple-document-views.md)。 如果没有，则它应显示相应的错误消息。

## <a name="see-also"></a>另请参阅
- [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)
- [自定义编辑器中的文档数据和文档视图](../extensibility/document-data-and-document-view-in-custom-editors.md)
