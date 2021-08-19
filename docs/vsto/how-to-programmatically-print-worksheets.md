---
title: 如何：以编程方式打印工作表
description: 了解如何使用 Visual Studio 以编程方式打印工作簿中Microsoft Excel工作表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- printing [Office development in Visual Studio], worksheets
- worksheets, printing
- print preview, worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: d02691d20748a9b982b30f49b1ec5426b7932e83
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122099745"
---
# <a name="how-to-programmatically-print-worksheets"></a>如何：以编程方式打印工作表

可以打印工作簿中的任何工作表。

[!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="print-a-worksheet-in-a-document-level-customization"></a>在文档级自定义项中打印工作表

### <a name="to-print-a-worksheet"></a>打印工作表

1. 先调用 `Sheet1` 的 `PrintOut` 方法，请求两个副本，然后预览文档，再进行打印。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet22":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet22":::

   <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A>方法使你能够在"打印预览"窗口中显示 **指定的** 对象。 以下代码假定你已具有一个名为 `Sheet1` 的 <xref:Microsoft.Office.Tools.Excel.Worksheet> 主机项。

### <a name="to-preview-a-page-before-printing"></a>在打印之前预览页面

1. 调用工作表的 <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A> 方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet23":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet23":::

## <a name="print-a-worksheet-in-a-vsto-add-in"></a>在外接程序中VSTO工作表

### <a name="to-print-a-worksheet"></a>打印工作表

1. 先调用活动工作表的 <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintOut%2A> 方法，请求两个副本，然后预览文档，再进行打印。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet14":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet14":::

   <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A>方法使你能够在"打印预览"窗口中显示 **指定的** 对象。

### <a name="to-preview-a-page-before-printing"></a>在打印之前预览页面

1. 调用活动工作表的 <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> 方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet15":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet15":::

## <a name="see-also"></a>请参阅

- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式检查工作表中的拼写](../vsto/how-to-programmatically-check-spelling-in-worksheets.md)
- [工作表宿主项](../vsto/worksheet-host-item.md)
- [对项目中对象的全局Office访问](../vsto/global-access-to-objects-in-office-projects.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
