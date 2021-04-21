---
title: 如何：创建和修改自定义文档属性
description: 如果要将其他信息与文档一起存储，请了解如何创建和修改自定义文档属性。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom document properties
- documents [Office development in Visual Studio], properties
- document properties [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cd89cb1e2991f48fefd9984eaa6d5894d9b506c1
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826572"
---
# <a name="how-to-create-and-modify-custom-document-properties"></a>如何：创建和修改自定义文档属性
  上面列出的 Microsoft Office 应用程序提供与文档存储在一起的内置属性。 此外，如果要将其他信息与文档一起存储，可以创建和修改自定义文档属性。

 [!INCLUDE[appliesto_docprops](../vsto/includes/appliesto-docprops-md.md)]

 使用文档的 CustomDocumentProperties 属性来处理自定义属性。 例如，在 Microsoft Office Excel 的文档级项目中，请使用 <xref:Microsoft.Office.Tools.Excel.Workbook.CustomDocumentProperties%2A> 类的 `ThisWorkbook` 属性。 在 Excel 的 VSTO 外接程序项目中，请使用 <xref:Microsoft.Office.Interop.Excel._Workbook.CustomDocumentProperties%2A> 对象的 <xref:Microsoft.Office.Interop.Excel.Workbook> 属性。 这些属性将返回 <xref:Microsoft.Office.Core.DocumentProperties> 对象，该对象为 <xref:Microsoft.Office.Core.DocumentProperty> 对象的集合。 可以使用集合的 `Item` 属性，按名称或索引检索该集合中的特定属性。

 下面的示例演示如何在 Excel 文档级自定义项中添加自定义属性并为其赋值。

## <a name="example"></a>示例
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb" id="Snippet6":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs" id="Snippet6":::

## <a name="robust-programming"></a>可靠编程
 尝试访问未定义的属性的 `Value` 属性会引发异常。

## <a name="see-also"></a>请参阅
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [程序文档级自定义项](../vsto/programming-document-level-customizations.md)
- [如何：读取和写入文档属性](../vsto/how-to-read-from-and-write-to-document-properties.md)
