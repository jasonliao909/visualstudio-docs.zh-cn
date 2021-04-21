---
title: 如何：以编程方式保存工作簿
description: 以编程方式保存 Microsoft Excel 工作簿而不更改路径并保存工作簿的副本，而不修改内存中打开的工作簿。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, saving in XML format
- workbooks, saving
- workbooks, saving backup copies
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4559d098a80a1dfd8f1d3f5c2c21cbebc992fcb7
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828977"
---
# <a name="how-to-programmatically-save-workbooks"></a>如何：以编程方式保存工作簿
  可通过多种方式保存工作簿。 可以保存工作簿而不更改路径。 如果以前没有保存过工作簿，则应该通过指定一个路径来保存工作簿。 如果没有显式路径，Microsoft Office Excel 会使用创建文件时为其指定的名称将文件保存在当前文件夹中。 还可以保存工作簿的副本，而不修改内存中打开的工作簿。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="save-a-workbook-without-changing-the-path"></a>保存工作簿而不更改路径

### <a name="to-save-a-workbook-associated-with-a-document-level-customization"></a>保存与文档级自定义项关联的工作簿

1. 调用 <xref:Microsoft.Office.Tools.Excel.Workbook.Save%2A> 类的 `ThisWorkbook` 方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb" id="Snippet4":::

### <a name="to-save-the-active-workbook-in-a-vsto-add-in"></a>在 VSTO 外接程序中保存活动工作簿

1. 调用 <xref:Microsoft.Office.Interop.Excel._Workbook.Save%2A> 方法以保存活动工作薄。 若要使用下面的代码示例，请在 Excel 的应用程序级项目内的 `ThisAddIn` 类中运行它。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet3":::

## <a name="save-a-workbook-with-a-new-path"></a>使用新路径保存工作簿
 可以将指定的工作簿保存到新位置或以新名称保存，还可以选择指定文件格式、密码和访问模式等。

> [!NOTE]
> 在 <xref:Microsoft.Office.Interop.Excel._Application.DisplayAlerts%2A> 使用新路径保存工作簿之前，您可能需要将属性设置为 **False** ，因为以某些格式保存需要交互。 如果将此属性设置为 **False** ，则 Excel 将使用所有默认值。

### <a name="to-save-a-workbook-associated-with-a-document-level-customization"></a>保存与文档级自定义项关联的工作簿

1. 调用 <xref:Microsoft.Office.Tools.Excel.Workbook.SaveAs%2A> 类的 `ThisWorkbook` 方法。 若要使用下面的代码示例，请在 `ThisWorkbook` 类中运行它。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb" id="Snippet5":::

### <a name="to-save-the-active-workbook-in-a-vsto-add-in"></a>在 VSTO 外接程序中保存活动工作簿

1. 调用 <xref:Microsoft.Office.Interop.Excel._Workbook.SaveAs%2A> 方法以将活动工作簿保存到新路径。 若要使用下面的代码示例，请在 Excel 的应用程序级项目内的 `ThisAddIn` 类中运行它。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet4":::

## <a name="save-a-copy-of-the-workbook"></a>保存工作簿的副本
 可以将工作簿的副本保存到文件中，而不修改内存中打开的工作簿。 当想要创建备份副本而不修改工作簿的位置时，此方法十分有用。

### <a name="to-save-a-workbook-associated-with-a-document-level-customization"></a>保存与文档级自定义项关联的工作簿

1. 调用 <xref:Microsoft.Office.Tools.Excel.Workbook.SaveCopyAs%2A> 类的 `ThisWorkbook` 方法。 若要使用下面的代码示例，请在 `ThisWorkbook` 类中运行它。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb" id="Snippet6":::

### <a name="to-save-the-active-workbook-in-a-vsto-add-in"></a>在 VSTO 外接程序中保存活动工作簿

1. 调用 <xref:Microsoft.Office.Interop.Excel._Workbook.SaveCopyAs%2A> 方法以保存活动工作簿的副本。 若要使用下面的代码示例，请在 Excel 的应用程序级项目内的 `ThisAddIn` 类中运行它。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet5":::

## <a name="robust-programming"></a>可靠编程
 以交互方式取消任何保存或复制工作簿的方法将在代码中引发运行时错误。 例如，如果您的过程调用了 <xref:Microsoft.Office.Tools.Excel.Workbook.SaveAs%2A> 方法但不禁用 Excel 中的提示，并且您的用户在出现提示时单击 " **取消** "，则 Excel 将引发运行时错误。

## <a name="see-also"></a>另请参阅
- [使用工作簿](../vsto/working-with-workbooks.md)
- [工作簿宿主项](../vsto/workbook-host-item.md)
- [如何：以编程方式关闭工作簿](../vsto/how-to-programmatically-close-workbooks.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
