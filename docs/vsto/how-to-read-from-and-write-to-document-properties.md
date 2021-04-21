---
title: 如何：读取和写入文档属性
description: 了解如何使用 Visual Studio 在 Microsoft Excel 和 Microsoft Word 中获取或设置文档属性。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], document properties
- documents [Office development in Visual Studio], properties
- document properties [Office development in Visual Studio]
- Excel [Office development in Visual Studio], document properties
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3474d86a7408e841d383c82e5ab38da90253dbbf
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826676"
---
# <a name="how-to-read-from-and-write-to-document-properties"></a>如何：读取和写入文档属性
  可以存储文档以及文档属性。 Office 应用程序提供了许多内置的属性，例如作者、标题和主题。 本主题演示如何在 Microsoft Office Excel 和 Microsoft Office Word 中设置文档属性。

 [!INCLUDE[appliesto_docprops](../vsto/includes/appliesto-docprops-md.md)]

## <a name="set-document-properties-in-excel"></a>在 Excel 中设置文档属性
 要使用 Excel 中的内置属性，请使用以下属性：

- 在文档级项目中，使用 <xref:Microsoft.Office.Tools.Excel.Workbook.BuiltinDocumentProperties%2A> 类的 `ThisWorkbook` 属性。

- 在 VSTO 外接程序项目中，使用 <xref:Microsoft.Office.Interop.Excel._Workbook.BuiltinDocumentProperties%2A> 对象的 <xref:Microsoft.Office.Interop.Excel.Workbook> 属性。

  这些属性将返回 <xref:Microsoft.Office.Core.DocumentProperties> 对象，该对象为 <xref:Microsoft.Office.Core.DocumentProperty> 对象的集合。 可以使用集合的 `Item` 属性，按名称或索引检索该集合中的特定属性。

  下面的代码示例演示了如何更改文档级项目中的内置 **Revision Number** 属性。

### <a name="to-change-the-revision-number-property-in-excel"></a>若要更改在 Excel 中的修订号属性

1. 将内置文档属性分配给变量。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs" id="Snippet7":::

2. 以 1 递增 `Revision Number` 属性。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb" id="Snippet8":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs" id="Snippet8":::

## <a name="set-document-properties-in-word"></a>在 Word 中设置文档属性
 若要使用 Word 中的内置属性，请使用以下属性：

- 在文档级项目中，使用 <xref:Microsoft.Office.Tools.Word.Document.BuiltInDocumentProperties%2A> 类的 `ThisDocument` 属性。

- 在 VSTO 外接程序项目中，使用 <xref:Microsoft.Office.Interop.Word._Document.BuiltInDocumentProperties%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Document> 属性。

  这些属性将返回 <xref:Microsoft.Office.Core.DocumentProperties> 对象，该对象为 <xref:Microsoft.Office.Core.DocumentProperty> 对象的集合。 可以使用集合的 `Item` 属性，按名称或索引检索该集合中的特定属性。

  下面的代码示例演示了如何更改文档级项目中的内置 **Subject** 属性。

### <a name="to-change-the-subject-property"></a>若要更改主题属性

1. 将内置文档属性分配给变量。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingWordCS/ThisDocument.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingWordVB/ThisDocument.vb" id="Snippet1":::

2. 将 `Subject` 属性更改为“白皮书”。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingWordCS/ThisDocument.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingWordVB/ThisDocument.vb" id="Snippet2":::

## <a name="robust-programming"></a>可靠编程
 这些示例假定已在 Excel 文档级项目的 `ThisWorkbook` 类中和 Word 文档级项目中的 `ThisDocument` 类中编写代码。

 虽然你可以使用 Word 和 Excel 及其对象，但 Microsoft Office 仍然提供了可用的内置文档属性的列表。 尝试访问未定义的属性会引发异常。

## <a name="see-also"></a>请参阅
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [程序文档级自定义项](../vsto/programming-document-level-customizations.md)
- [如何：创建和修改自定义文档属性](../vsto/how-to-create-and-modify-custom-document-properties.md)
