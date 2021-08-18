---
title: 如何：以编程方式将新工作表添加到工作簿
description: 了解如何以编程方式创建工作表，然后将工作表添加到工作簿中的工作表集合。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, adding worksheets
- workbooks, creating worksheets
- worksheets, creating
- worksheets, adding to workbooks
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 171608021bb967306a89e22bff68c7d3cd3ce639
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122026247"
---
# <a name="how-to-programmatically-add-new-worksheets-to-workbooks"></a>如何：以编程方式将新工作表添加到工作簿
  可以通过编程方式创建一个工作表，然后将它添加到工作簿中工作表的集合。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-add-a-new-worksheet-to-a-workbook-in-a-document-level-customization"></a>将新工作表添加到文档级自定义项中的工作簿

1. 使用 <xref:Microsoft.Office.Interop.Excel.Worksheets.Add%2A> 集合的 <xref:Microsoft.Office.Interop.Excel.Sheets> 方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet15":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet15":::

     新工作表是一个本机 <xref:Microsoft.Office.Interop.Excel.Worksheet> 对象，不是主机项。 如果想要添加 <xref:Microsoft.Office.Tools.Excel.Worksheet> 主机项，则应在设计时添加工作表。

## <a name="to-add-a-new-worksheet-to-a-workbook-in-a-vsto-add-in"></a>将新工作表添加到 VSTO 外接程序中的工作簿

1. 使用 <xref:Microsoft.Office.Interop.Excel.Worksheets.Add%2A> 集合的 <xref:Microsoft.Office.Interop.Excel.Sheets> 方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet11":::

     新工作表是一个本机 <xref:Microsoft.Office.Interop.Excel.Worksheet> 对象，不是主机项。 你还可以从本机 <xref:Microsoft.Office.Tools.Excel.Worksheet> 对象生成 <xref:Microsoft.Office.Interop.Excel.Worksheet> 主机项。 有关详细信息，请参阅 [Extending Word Documents and Excel Workbooks in VSTO Add-ins at Run Time](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [如何：以编程方式从工作簿中删除工作表](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [如何：以编程方式选择工作表](../vsto/how-to-programmatically-select-worksheets.md)
- [使用Excel对象自动执行自动执行](../vsto/automating-excel-by-using-extended-objects.md)
- [对项目中对象的全局Office访问](../vsto/global-access-to-objects-in-office-projects.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
