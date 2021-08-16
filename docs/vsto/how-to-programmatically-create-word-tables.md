---
title: 如何：以编程方式创建 Word 表
description: 了解如何使用 Tables 集合的 Add 方法在表文档中的指定Microsoft Word表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], adding tables
- tables [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: ffa70b09b233f2f674c457999c6c7669332c100606c2be6f0c3802c967da154b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121408729"
---
# <a name="how-to-programmatically-create-word-tables"></a>如何：以编程方式创建 Word 表
  <xref:Microsoft.Office.Interop.Word.Tables> 集合是 <xref:Microsoft.Office.Interop.Word.Document>、<xref:Microsoft.Office.Tools.Word.Document>、<xref:Microsoft.Office.Interop.Word.Selection> 和 <xref:Microsoft.Office.Interop.Word.Range> 类的成员，这意味着可以在上述任一上下文中创建表格。 使用 <xref:Microsoft.Office.Interop.Word.Tables> 集合的 <xref:Microsoft.Office.Interop.Word.Tables.Add%2A> 方法在指定范围内添加表格。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="create-tables-in-document-level-customizations"></a>在文档级自定义项中创建表

### <a name="to-add-a-table-to-a-document"></a>向文档添加表

- 使用 <xref:Microsoft.Office.Interop.Word.Tables.Add%2A> 方法在文档开头添加一个三行四列的表格。

   若要使用下面的代码示例，请从项目的 `ThisDocument` 类中运行它。

   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet86":::
   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet86":::

  在创建表格时，表格会自动添加到 <xref:Microsoft.Office.Tools.Word.Document> 主机项的 <xref:Microsoft.Office.Interop.Word.Tables> 集合中。 然后，可以使用 <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> 属性按照项编号引用该表格，如以下代码所示。

### <a name="to-refer-to-a-table-by-item-number"></a>按照项编号引用表格

1. 使用 <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> 属性并提供要引用的表格的项编号。

    若要使用下面的代码示例，请从项目的 `ThisDocument` 类中运行它。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet87":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet87":::

   每个 <xref:Microsoft.Office.Interop.Word.Table> 对象还具有一个 <xref:Microsoft.Office.Interop.Word.Table.Range%2A> 属性，该属性可用于设置格式属性。

### <a name="to-apply-a-style-to-a-table"></a>将样式应用到表格

1. 使用 <xref:Microsoft.Office.Interop.Word.Table.Style%2A> 属性将其中一个 Word 内置样式应用到表格。

     若要使用下面的代码示例，请从项目的 `ThisDocument` 类中运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet88":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet88":::

## <a name="create-tables-in-vsto-add-ins"></a>在外接程序VSTO创建表

### <a name="to-add-a-table-to-a-document"></a>向文档添加表

- 使用 <xref:Microsoft.Office.Interop.Word.Tables.Add%2A> 方法在文档开头添加一个三行四列的表格。

   下面的代码示例是向活动文档添加一个表格。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行它。

   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet86":::
   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet86":::

  在创建表格时，表格会自动添加到 <xref:Microsoft.Office.Interop.Word.Document> 的 <xref:Microsoft.Office.Interop.Word.Tables> 集合中。 然后，可以使用 <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> 属性按照项编号引用该表格，如以下代码所示。

### <a name="to-refer-to-a-table-by-item-number"></a>按照项编号引用表格

1. 使用 <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> 属性并提供要引用的表格的项编号。

    下面的代码示例使用活动文档。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行它。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet87":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet87":::

   每个 <xref:Microsoft.Office.Interop.Word.Table> 对象还具有一个 <xref:Microsoft.Office.Interop.Word.Table.Range%2A> 属性，该属性可用于设置格式属性。

### <a name="to-apply-a-style-to-a-table"></a>将样式应用到表格

1. 使用 <xref:Microsoft.Office.Interop.Word.Table.Style%2A> 属性将其中一个 Word 内置样式应用到表格。

     下面的代码示例使用活动文档。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet88":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet88":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式向 Word 表中的单元格添加文本和格式设置](../vsto/how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables.md)
- [如何：以编程方式将行和列添加到 Word 表](../vsto/how-to-programmatically-add-rows-and-columns-to-word-tables.md)
- [如何：以编程方式使用文档属性填充 Word 表](../vsto/how-to-programmatically-populate-word-tables-with-document-properties.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
