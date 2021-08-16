---
title: 如何：以编程方式打印文档
description: 了解如何将整个 Microsoft Word 文档或文档的一部分打印到默认打印机。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], printing documents
- documents [Office development in Visual Studio], printing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 31b6bf4e9fa4041710da1269ff239eecb3e75749e1819144fc99fed5f198efb5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121408118"
---
# <a name="how-to-programmatically-print-documents"></a>如何：以编程方式打印文档
  你可以将整个 Microsoft Office Word 文档或文档的一部分打印到默认打印机。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="print-a-document-that-is-part-of-a-document-level-customization"></a>打印属于文档级自定义项的文档

### <a name="to-print-the-entire-document"></a>若要打印整个文档

1. 调用项目中 <xref:Microsoft.Office.Tools.Word.Document.PrintOut%2A> 类的 `ThisDocument` 方法以打印整个文档。 若要使用此示例，请在 `ThisDocument` 类中运行代码。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet11":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet11":::

### <a name="to-print-the-current-page-of-the-document"></a>若要打印文档的当前页面

1. 调用项目中 <xref:Microsoft.Office.Tools.Word.Document.PrintOut%2A> 类的 `ThisDocument` 方法并指定打印一份当前页面。 若要使用此示例，请在 `ThisDocument` 类中运行代码。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet12":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet12":::

## <a name="print-a-document-by-using-a-vsto-add-in"></a>使用 VSTO 外接程序打印文档

### <a name="to-print-an-entire-document"></a>若要打印整个文档

1. 调用要打印的 <xref:Microsoft.Office.Interop.Word._Document.PrintOut%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Document> 方法。 下面的代码示例将打印活动文档。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行代码。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet11":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet11":::

### <a name="to-print-the-current-page-of-a-document"></a>若要打印文档的当前页面

1. 调用要打印的 <xref:Microsoft.Office.Interop.Word._Document.PrintOut%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Document> 方法，并指定打印一份当前页面。 下面的代码示例将打印活动文档。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行代码。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet12":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet12":::

## <a name="see-also"></a>请参阅
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
