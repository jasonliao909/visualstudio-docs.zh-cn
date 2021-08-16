---
title: 如何：以编程方式创建新文档
description: 了解如何使用 Visual Studio 以编程方式在 Microsoft Word 中创建新文档。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- templates [Office development in Visual Studio], custom document
- Word [Office development in Visual Studio], creating documents
- documents [Office development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 82ca1781314585ef15fdf73e33e106108bf2c5a5e0b433eb9ae94adfa9025a2a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121423899"
---
# <a name="how-to-programmatically-create-new-documents"></a>如何：以编程方式创建新文档
  当以编程方式创建文档时，新文档是一个本机 <xref:Microsoft.Office.Interop.Word.Document> 对象。 此对象不具有 <xref:Microsoft.Office.Tools.Word.Document> 主机项的其他事件和数据绑定功能。 有关详细信息，请参阅 [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 开发文档级项目时，不能以编程方式将 <xref:Microsoft.Office.Tools.Word.Document> 主机项添加到你的项目。 在 VSTO 外接程序项目中，可在运行时将任意 <xref:Microsoft.Office.Interop.Word.Document> 对象转换为 <xref:Microsoft.Office.Tools.Word.Document> 主机项。 有关详细信息，请参阅在[运行时 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

## <a name="to-create-a-new-document-based-on-the-normal-template"></a>基于 Normal 模板创建新文档

- 使用 <xref:Microsoft.Office.Interop.Word.Documents> 集合的 <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> 方法来创建基于 Normal 模板的新文档。 若要使用此代码模板，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet1":::

## <a name="use-custom-templates"></a>使用自定义模板
 此 <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> 方法具有一个可选的 *模板* 自变量，可基于模板而不是 Normal 模板来创建新文档。 你必须提供模板的文件名称和完全限定路径。

### <a name="to-create-a-new-document-based-on-a-custom-template"></a>基于自定义模板创建新文档

- 调用 <xref:Microsoft.Office.Interop.Word.Documents> 集合的 <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> 方法，并指定模板的路径。 若要使用此代码模板，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet2":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式打开现有文档](../vsto/how-to-programmatically-open-existing-documents.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
