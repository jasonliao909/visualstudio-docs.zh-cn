---
title: 如何：以编程方式添加和删除工作表注释
description: 了解如何以编程方式在 Microsoft Office Excel 工作表中添加和删除注释。 只能将注释添加到单个单元，而不能添加到多单元格范围。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, comments
- worksheets, comments
- comments, worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 04259cdb6f21254dba6c7769347403fbb6410f26
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122148150"
---
# <a name="how-to-programmatically-add-and-delete-worksheet-comments"></a>如何：以编程方式添加和删除工作表注释
  可以以编程方式在 Microsoft Office Excel 工作表中添加和删除注释。 可以仅向单个单元格而非多单元格区域添加注释。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="add-and-delete-a-comment-in-a-document-level-project"></a>在文档级项目中添加和删除注释
 下面的示例假定名为 <xref:Microsoft.Office.Tools.Excel.NamedRange> 的工作表上存在名为 `dateComment` 的单单元格 `Sheet1`控件。

### <a name="to-add-a-new-comment-to-a-named-range"></a>向命名区域添加新的注释

1. 调用 <xref:Microsoft.Office.Tools.Excel.NamedRange.AddComment%2A> 控件的 <xref:Microsoft.Office.Tools.Excel.NamedRange> 方法并提供注释文本。 必须将此代码置于 `Sheet1` 类中。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet30":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet30":::

#### <a name="to-delete-a-comment-from-a-named-range"></a>删除命名区域中的注释

1. 验证区域中是否存在注释并将其删除。 必须将此代码置于 `Sheet1` 类中。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet29":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet29":::

## <a name="add-and-delete-a-comment-in-a-vsto-add-in-project"></a>在 VSTO 外接程序项目中添加和删除注释
 下面的示例假定活动的工作表上存在名为 <xref:Microsoft.Office.Interop.Excel.Range> 的单单元格 `dateComment` 。

### <a name="to-add-a-new-comment-to-an-excel-range"></a>向 Excel 区域添加新的注释

1. 调用 <xref:Microsoft.Office.Interop.Excel.Range.AddComment%2A> 的 <xref:Microsoft.Office.Interop.Excel.Range> 方法并提供注释文本。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet20":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet20":::

### <a name="to-delete-a-comment-from-an-excel-range"></a>删除 Excel 区域中的注释

1. 验证区域中是否存在注释并将其删除。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet19":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet19":::

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式显示工作表注释](../vsto/how-to-programmatically-display-worksheet-comments.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
