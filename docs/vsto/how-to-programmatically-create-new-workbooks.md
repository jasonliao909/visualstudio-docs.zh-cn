---
title: 如何：以编程方式创建新工作簿
description: 了解如何使用 Visual Studio 以编程方式创建新的 Microsoft Excel 工作簿。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], creating workbooks
- workbooks, creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: dded73f4af9221b096adc7c0cfda8c70fb91a348
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046581"
---
# <a name="how-to-programmatically-create-new-workbooks"></a>如何：以编程方式创建新工作簿
  以编程方式创建工作簿时，它是一个本机 <xref:Microsoft.Office.Interop.Excel.Workbook> 对象，而不是 <xref:Microsoft.Office.Tools.Excel.Workbook> 主机项。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 你可以在 VSTO 外接程序项目中为 <xref:Microsoft.Office.Interop.Excel.Workbook> 对象生成一个 <xref:Microsoft.Office.Tools.Excel.Workbook> 主机项。 有关详细信息，请参阅扩展[Word 文档和Excel运行时VSTO外接程序中的工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

## <a name="to-create-a-new-workbook"></a>创建新的工作簿

1. 使用 <xref:Microsoft.Office.Interop.Excel.Workbooks.Add%2A> 集合的 <xref:Microsoft.Office.Interop.Excel.Workbooks> 方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet1":::

    > [!NOTE]
    > 通过将想要用作参数的模板传递给 <xref:Microsoft.Office.Interop.Excel.Workbooks.Add%2A> 方法，可以基于该模板而不是默认模板创建工作簿。

## <a name="see-also"></a>请参阅
- [在外接程序Excel扩展 Word 文档VSTO工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [运行时向Office文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [使用工作簿](../vsto/working-with-workbooks.md)
- [如何：以编程方式打开工作簿](../vsto/how-to-programmatically-open-workbooks.md)
- [如何：以编程方式保存工作簿](../vsto/how-to-programmatically-save-workbooks.md)
- [如何：以编程方式关闭工作簿](../vsto/how-to-programmatically-close-workbooks.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
