---
title: 如何：以编程方式选择工作表
description: 使用 Visual Studio 以编程方式选择 Excel 工作簿的工作表宿主项或表集合 Microsoft Excel 工作表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, selecting
- Excel projects, selecting worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 82d74fff713741208981278474b295c17975a639
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122032727"
---
# <a name="how-to-programmatically-select-worksheets"></a>如何：以编程方式选择工作表
  <xref:Microsoft.Office.Tools.Excel.Worksheet.Select%2A> 方法选择指定的对象，从而将用户的选择移到新对象上。 如果想要将焦点移到对象上，而不更改用户的选择，请使用 <xref:Microsoft.Office.Tools.Excel.Worksheet.Activate%2A> 方法。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 如果要在 VSTO 外接程序中选择现有工作表，或者如果工作表是在运行时在文档级自定义项中创建的，则必须使用 Excel 工作簿的 Excel 集合来访问该工作 <xref:Microsoft.Office.Interop.Excel.Sheets> 簿; 否则，可以直接访问该 <xref:Microsoft.Office.Tools.Excel.Worksheet> 主机项。

## <a name="use-the-worksheet-host-item"></a>使用工作表主机项
 在文档级自定义项中，将以下代码添加到 *Sheet1 .vb* 或 *sheet1. cs*。

### <a name="to-select-the-first-worksheet-in-a-workbook-using-a-host-item"></a>使用主机项选择工作簿中的第一个工作表

1. 调用 <xref:Microsoft.Office.Tools.Excel.Worksheet.Select%2A> 的 `Sheet1`方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet19":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet19":::

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>使用 Excel 工作簿的表集合
 使用 Excel <xref:Microsoft.Office.Interop.Excel.Sheets> 集合访问工作表。

### <a name="to-select-the-first-worksheet-in-a-workbook-using-the-sheets-collection-of-the-excel-workbook"></a>使用 Excel 工作簿的 Sheets 集合选择工作簿中的第一个工作表

1. 调用 <xref:Microsoft.Office.Interop.Excel.Sheets> 集合的 <xref:Microsoft.Office.Interop.Excel.Sheets.Select%2A> 方法来选择活动工作薄中的第一个工作表。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet20":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet20":::

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式打印工作表](../vsto/how-to-programmatically-print-worksheets.md)
- [如何：以编程方式从工作簿中删除工作表](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [如何：以编程方式隐藏工作表](../vsto/how-to-programmatically-hide-worksheets.md)
- [如何：以编程方式保护工作表](../vsto/how-to-programmatically-protect-worksheets.md)
- [工作表宿主项](../vsto/worksheet-host-item.md)
- [Office 项目中对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
