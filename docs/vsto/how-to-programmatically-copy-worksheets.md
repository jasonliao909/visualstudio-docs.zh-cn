---
title: 如何：以编程方式复制工作表
description: 了解如何创建工作表的副本，并在工作簿中的现有工作表之前或之后插入该工作表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, copying
- Excel [Office development in Visual Studio], copying worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 7aed53b3579e656d3b00e200b38075859174b8cf
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122106194"
---
# <a name="how-to-programmatically-copy-worksheets"></a>如何：以编程方式复制工作表
  你可以创建一份工作表的副本，并将该工作表插入工作簿中现有的工作表之前或之后。 如果不指定要插入工作表的位置，则 Excel 将创建一个新的工作簿来容纳新工作表。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

> [!NOTE]
> 无论是以编程方式复制工作表，还是最终用户手动复制工作表，新工作表都没有代码，并且新工作表上的控件无法运行。 这是因为新复制的工作表是 <xref:Microsoft.Office.Interop.Excel.Worksheet> 对象而不 <xref:Microsoft.Office.Tools.Excel.Worksheet> 主机项。 Windows 窗体控件和主机控件仅可以添加到主机项。 有关详细信息，请参阅 [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)。

## <a name="to-add-a-copied-worksheet-to-a-workbook-in-a-document-level-customization"></a>将复制的工作表添加到文档级自定义项中的工作簿

1. 使用 <xref:Microsoft.Office.Interop.Excel.Worksheets.Copy%2A> 方法复制当前工作簿中的第一个工作表并将副本放在第三个工作表后。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet16":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet16":::

## <a name="to-add-a-copied-worksheet-to-a-workbook-in-a-vsto-add-in"></a>将复制的工作表添加到 VSTO 外接程序中的工作簿

1. 使用 <xref:Microsoft.Office.Interop.Excel.Worksheets.Copy%2A> 方法复制当前工作簿中的第一个工作表并将副本放在第三个工作表后。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet12":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet12":::

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [如何：以编程方式向工作簿添加新工作表](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [如何：以编程方式从工作簿中删除工作表](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [如何：以编程方式选择工作表](../vsto/how-to-programmatically-select-worksheets.md)
- [使用扩展对象自动 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [Office 项目中对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
